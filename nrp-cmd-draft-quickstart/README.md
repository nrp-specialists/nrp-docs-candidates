<!-- cSpell:language cs -->
# Vložení nového záznamu do datarepo.eosc.cz pomocí `nrp-cmd`

Postup pro vytvoření nepublikovaného záznamu (draftu) s připojeným souborem
v datovém Catch-all repozitáři [datarepo.eosc.cz](https://datarepo.eosc.cz). 
Záznamy se zakládají podle modelu `datasets` v1.1.0 (CCMM).

Dokumentace nástroje: <https://nrp-cz.github.io/docs/userguide/commandline>

V tomto adresáři jsou dva soubory, s nimiž postup pracuje:

| soubor | co to je |
| --- | --- |
| `catch-all-sample-record.json` | ukázková metadata datové sady |
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

Kontrola: `nrp-cmd list repositories`.

## 2. Metadata

Povinné minimum:

| pole | poznámka |
| --- | --- |
| `metadata.title` | |
| `metadata.publication_date` | |
| `metadata.creators` | |
| `metadata.resource_type` | pro datovou sadu `{"id": "c_ddb1"}` |
| `metadata.publisher` | jednoduchý string, **nutný pro registraci DOI** |

`metadata.publisher` schéma neuvádí jako povinný, draft se bez něj založí, ale 
s evidovanou chybou, proto je lepší vyplnit údaj hned.

Slovníková pole se zadávají jako `{"id": "…"}`. Když ID neodpovídá slovníku,
API vrátí `400 Invalid value <hodnota>` a skončí na první chybě. Konvence se
mezi slovníky liší — typy názvů jsou kebab-case (`translated-title`,
`subtitle`), typy dat CamelCase (`Collected`, `Available`). Platná ID
nejspolehlivěji zjistíte z publikovaných záznamů:

```bash
curl -s "https://datarepo.eosc.cz/api/datasets?size=100" \
  | jq -r '.hits.hits[].metadata.additional_titles[]?.type.id' | sort -u
```

Ukázkový `catch-all-sample-record.json` obsahuje i nepovinné bloky — překlad
názvu, abstrakt, předměty, licenci, financování a související zdroje. Fiktivní
DOI v `identifiers` a `funding[0].award.number` jsou placeholdery k nahrazení.

## 3. Založení draftu se souborem

```bash
nrp-cmd create record --repository catch-all --model datasets \
  --workflow individual \
  ./catch-all-sample-record.json \
  ./dummy.txt '{"title": "Ukázkový datový soubor"}'
```

- **Cesta k metadatům musí začínat `./` nebo `/`**, jinak nástroj argument
  považuje za doslovný JSON string.
- Metadata se předávají jako celý dokument, tedy `{"metadata": {…}}`.
- Soubory se uvádějí v párech `cesta` + `metadata souboru`, párů může být víc.
- `--workflow individual` zakládá záznam mimo community; pro záznam
  v community použijte `--community <slug>`.

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
jq '.metadata' catch-all-sample-record.json > inner-metadata.json
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

## 6. Publikování

Draft je do publikování privátní a má `expires_at`, takže po nějaké době zmizí sám.

Publikování neprobíhá přes `links.publish`; u workflow `individual` se zakládá
požadavek typu `publish_draft`. Absence `publish` v `links` tedy není závada.
Jaké požadavky lze na záznam podat:

```bash
curl -s -H "Authorization: Bearer <TOKEN>" \
  "https://datarepo.eosc.cz/api/requests/applicable?topic=record:<ID>" | jq .
```

Publikování registruje DOI a zveřejní záznam, je tedy nevratná.

## Známé potíže

**`locations…geometry` se zahazuje.** GeoJSON geometrie se neuloží, `place`
přežije. Je to chyba v `oarepo-model` (typ `dynamic-object` serializuje na
prázdný objekt), ne v datech. Ukázkový JSON proto uvádí jen `place`.
