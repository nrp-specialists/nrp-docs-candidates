# Vložení nového záznamu do datarepo.eosc.cz pomocí `nrp-cmd`

Postup pro vytvoření nepublikovaného záznamu (draftu) s připojeným souborem
v repozitáři [datarepo.eosc.cz](https://datarepo.eosc.cz), tedy katalogovém
repozitáři NRP pro česká vědecká data. Záznamy se zakládají podle modelu
`datasets` v1.1.0 (CCMM).

Dokumentace nástroje: <https://nrp-cz.github.io/docs/userguide/commandline>

V tomto adresáři jsou dva soubory, se kterými postup pracuje:

| soubor | co to je |
| --- | --- |
| `catch-all-share.json` | ukázková metadata datové sady |
| `dummy.txt` | dummy datový soubor k připojení |

## 1. Instalace a token

```bash
uv tool install nrp-cmd
```

Token si vytvořte na <https://datarepo.eosc.cz/account/settings/applications/tokens/new>
a zaregistrujte repozitář:

```bash
nrp-cmd add repository https://datarepo.eosc.cz catch-all \
  --token <TOKEN> --no-launch-browser
```

Bez `--token` se nástroj pokusí otevřít prohlížeč a čeká na ruční vložení
tokenu, což vyžaduje terminál s TTY — ve skriptu ani v CI to neprojde.

Kontrola: `nrp-cmd list repositories`. Konfigurace se ukládá do
`~/.nrp/invenio-config.json` a reinstalace nástroje o tokeny nepřipraví.

## 2. Metadata

Povinné minimum:

| pole | poznámka |
| --- | --- |
| `metadata.title` | |
| `metadata.publication_date` | |
| `metadata.creators` | |
| `metadata.resource_type` | pro datovou sadu `{"id": "c_ddb1"}` |
| `metadata.publisher` | jednoduchý string, **nutný pro registraci DOI** |

`metadata.publisher` schéma neuvádí jako povinný, ale bez něj publikace selže
na `Missing publisher field required for DOI registration`. Vyplňte ho hned.

Slovníková pole se zadávají jako `{"id": "…"}`. Když ID neodpovídá slovníku,
API vrátí `400 Invalid value <hodnota>` a skončí na první chybě. Konvence se
mezi slovníky liší — typy názvů jsou kebab-case (`translated-title`,
`subtitle`), typy dat CamelCase (`Collected`, `Available`). Platná ID
nejspolehlivěji zjistíte z publikovaných záznamů:

```bash
curl -s "https://datarepo.eosc.cz/api/datasets?size=100" \
  | jq -r '.hits.hits[].metadata.additional_titles[]?.type.id' | sort -u
```

Ukázkový `catch-all-share.json` obsahuje i nepovinné bloky — překlad názvu,
abstrakt, předměty, licenci, financování a související zdroje. Fiktivní DOI
v `identifiers` a `funding[0].award.number` jsou placeholdery k nahrazení.

## 3. Založení draftu se souborem

```bash
nrp-cmd create record --repository catch-all --model datasets \
  --workflow individual \
  ./catch-all-share.json \
  ./dummy.txt '{"title": "Ukázkový datový soubor"}'
```

- **Cesta k metadatům musí začínat `./` nebo `/`**, jinak nástroj argument
  považuje za doslovný JSON string.
- Metadata se předávají jako celý dokument, tedy `{"metadata": {…}}`.
- Soubory se uvádějí v párech `cesta` + `metadata souboru`, párů může být víc.
- `--workflow individual` zakládá záznam mimo community; pro záznam
  v community použijte `--community <slug>`.
- Bez souborů přidejte `--metadata-only`.

Výstup příkazu uvádí `"files": {"count": 0}`, i když upload proběhl — odpověď
se serializuje před dokončením nahrávání.

## 4. Kontrola

```bash
nrp-cmd list files <ID> --repository catch-all --draft
```

Velikost musí odpovídat lokálnímu souboru.

**Vždycky se podívejte na pole `errors`.** Server do něj hlásí zahozená
i neznámá pole, aniž by request selhal, a návratový kód zůstane 0:

```bash
nrp-cmd get record <ID> --repository catch-all --draft -f json -o /tmp/rec.json
jq '.errors' /tmp/rec.json
```

Draft si prohlédnete na `https://datarepo.eosc.cz/datasets/uploads/<ID>`.

## 5. Úpravy

`update record` bere **jen obsah `metadata`**, ne celý dokument — opačně než
`create record`. Při poslání celého dokumentu server odpoví
`metadata.metadata: Unknown field` a metadata draftu vyprázdní:

```bash
jq '.metadata' catch-all-share.json > inner-metadata.json
nrp-cmd update record <ID> ./inner-metadata.json --repository catch-all --draft
```

Obsah souboru se mění smazáním a novým nahráním; `files update` mění pouze
metadata souboru. Smazání draftu vyžaduje `--draft`, jinak nástroj hledá
publikovaný záznam a vrátí `404 The persistent identifier is not registered`:

```bash
nrp-cmd files delete <ID> dummy.txt --repository catch-all --draft
nrp-cmd files upload <ID> ./dummy.txt '{"title": "…"}' --repository catch-all --draft
nrp-cmd delete record <ID> --repository catch-all --draft
```

## 6. Publikace

Draft je do publikace privátní a má `expires_at`, takže po nějaké době zmizí sám.

Publikace neprobíhá přes `links.publish`; u workflow `individual` se zakládá
požadavek typu `publish_draft`. Absence `publish` v `links` tedy není závada.
Jaké požadavky lze na záznam podat:

```bash
curl -s -H "Authorization: Bearer <TOKEN>" \
  "https://datarepo.eosc.cz/api/requests/applicable?topic=record:<ID>" | jq .
```

Publikace registruje DOI a zveřejní záznam, je tedy nevratná.

## Známé potíže

**`403 Permission denied` při zakládání záznamu.** Token nepatří datarepu.
Invenio neznámý token nezamítne, ale potichu degraduje na anonymní přístup,
takže čtení dál vypadá funkčně. Pokud pracujete s víc instancemi NRP, snadno
se zamění.

**Warning `The parameter --log-stacktrace is used more than once`.** Chyba
v `nrp-cmd` 0.9.0, na funkci nemá vliv. Potlačí se nastavením
`PYTHONWARNINGS='ignore:The parameter --log-stacktrace is used more than once:UserWarning'`.

**`locations…geometry` se zahazuje.** GeoJSON geometrie se neuloží, `place`
přežije. Je to chyba v `oarepo-model` (typ `dynamic-object` serializuje na
prázdný objekt), ne v datech. Ukázkový JSON proto uvádí jen `place`.
