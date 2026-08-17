# Založení draftu a nahrání souboru pomocí `nrp-cmd`

Postup pro vytvoření nepublikovaného záznamu (draftu) s připojeným souborem
v repozitáři postaveném na CESNET Invenio. Příklady jsou proti katalogovému
repozitáři [datarepo.eosc.cz](https://datarepo.eosc.cz), ale platí pro
kteroukoli instanci — mění se jen URL a alias.

Referenční dokumentace nástroje:
<https://nrp-cz.github.io/docs/userguide/commandline>

V tomto adresáři jsou dva ukázkové soubory, se kterými postup pracuje:

| soubor | co to je |
| --- | --- |
| `catch-all-share.json` | metadata datové sady podle modelu `datasets` v1.1.0 (CCMM) |
| `dummy.txt` | dummy datový soubor, který se k záznamu připojí |

## 1. Instalace

```bash
uv tool install nrp-cmd
```

Tím vznikne izolovaná instalace s příkazem v `~/.local/bin/nrp-cmd`.
Aktualizace pak `uv tool upgrade nrp-cmd`.

Nepoužívejte alias na binárku ve vlastním virtualenvu — alias přebije to,
co je nainstalované přes `uv`, a snadno pak ladíte jinou verzi, než si myslíte.
Ověření: `type nrp-cmd` musí vrátit cestu, ne `aliased to …`.

## 2. Token

Token si vytvořte **na té instanci, do které budete ukládat**:

<https://datarepo.eosc.cz/account/settings/applications/tokens/new>

> **Nejčastější chyba celého postupu.** Token z jiné instance NRP nevede
> na chybu autentizace — Invenio neznámý bearer token potichu degraduje na
> anonymního uživatele a `POST` skončí `403 Permission denied`. Čtecí operace
> přitom vypadají, že fungují, protože většina GET endpointů je veřejná.
>
> Ověření, že token instance opravdu přijímá — anonymně musí vrátit `403`,
> s tokenem `200`:
>
> ```bash
> curl -s -o /dev/null -w "%{http_code}\n" \
>   https://datarepo.eosc.cz/api/user/communities
> curl -s -o /dev/null -w "%{http_code}\n" \
>   -H "Authorization: Bearer <TOKEN>" \
>   https://datarepo.eosc.cz/api/user/communities
> ```

## 3. Registrace repozitáře

```bash
nrp-cmd add repository https://datarepo.eosc.cz catch-all \
  --token <TOKEN> --no-launch-browser
```

Bez `--token` se nástroj pokusí otevřít prohlížeč a čeká, až token vložíte
ručně — to potřebuje terminál s TTY, takže to neprojde ve skriptu ani v CI.

Přidejte `--default`, jen pokud má být tato instance výchozí pro všechny
příkazy. Pokud pracujete i s lokálním vývojovým repozitářem, výchozí alias
raději nenastavujte a předávejte `--repository` explicitně; jinak vám příkaz
bez toho přepínače tiše zamíří jinam.

Kontrola: `nrp-cmd list repositories`.

Konfigurace se ukládá do `~/.nrp/invenio-config.json` a je nezávislá na
instalaci nástroje — reinstalace `nrp-cmd` o tokeny nepřipraví.

## 4. Metadata

Minimum, které model `datasets` v1.1.0 vyžaduje:

| pole | poznámka |
| --- | --- |
| `metadata.title` | |
| `metadata.publication_date` | |
| `metadata.creators` | |
| `metadata.resource_type` | pro datovou sadu `{"id": "c_ddb1"}` |
| `metadata.publisher` | jednoduchý string, **nutný pro registraci DOI** |

`metadata.publisher` schéma neuvádí jako povinný, ale bez něj publikace
selže na `Missing publisher field required for DOI registration`. Vyplňte
ho hned, ať to nezjistíte až na konci.

Slovníková pole se zadávají jako `{"id": "…"}` a ID musí přesně odpovídat
slovníku instance. Když se neshoduje, API vrátí `400 Invalid value <hodnota>`
a **skončí na první chybě** — víc vadných hodnot tedy odladíte jen postupně.
Platná ID nejspolehlivěji zjistíte z už publikovaných záznamů:

```bash
curl -s "https://datarepo.eosc.cz/api/datasets?size=100" \
  | jq -r '.hits.hits[].metadata.additional_titles[]?.type.id' | sort -u
```

Pozor, že části slovníků mají různé konvence: typy názvů jsou kebab-case
(`translated-title`, `subtitle`), zatímco typy dat jsou CamelCase
(`Collected`, `Available`, `Issued`).

Ukázkový `catch-all-share.json` obsahuje i nepovinné bloky — překlad názvu,
abstrakt, předměty, licenci, financování a související zdroje. Fiktivní DOI
v `identifiers` a `funding[0].award.number` jsou placeholdery, které je
potřeba nahradit nebo smazat.

## 5. Založení draftu s připojeným souborem

```bash
nrp-cmd create record --repository catch-all --model datasets \
  --workflow individual \
  ./catch-all-share.json \
  ./dummy.txt '{"title": "Ukázkový datový soubor"}'
```

Na co si dát pozor:

- **Cesta k metadatům musí začínat `./` nebo `/`.** Bez toho nástroj argument
  považuje za doslovný JSON string, ne za cestu k souboru.
- **Metadata se předávají jako celý dokument**, tedy `{"metadata": {…}}`.
- **Soubory se uvádějí v párech** `cesta` + `metadata souboru`. Párů může být
  víc za sebou.
- `--workflow individual` zakládá záznam mimo community. Pro záznam
  v community použijte `--community <slug>`.
- Bez souborů přidejte `--metadata-only`.

> Výstup příkazu obsahuje `"files": {"count": 0}`, i když upload proběhl —
> odpověď se serializuje před dokončením nahrávání. Skutečný stav zjistíte
> až samostatným dotazem.

## 6. Kontrola

```bash
nrp-cmd list files <ID> --repository catch-all --draft
```

Velikost musí odpovídat lokálnímu souboru.

**Vždycky se podívejte na pole `errors`.** Server do něj hlásí zahozená
i neznámá pole, aniž by request selhal — `nrp-cmd` na ně neupozorní a návratový
kód je 0:

```bash
nrp-cmd get record <ID> --repository catch-all --draft -f json -o /tmp/rec.json
jq '.errors' /tmp/rec.json
```

Draft si prohlédnete na `https://datarepo.eosc.cz/datasets/uploads/<ID>`.

## 7. Úpravy

Změna metadat existujícího draftu bere **jen obsah `metadata`**, ne celý
dokument — to je opačně než u `create record`:

```bash
jq '.metadata' catch-all-share.json > inner-metadata.json
nrp-cmd update record <ID> ./inner-metadata.json --repository catch-all --draft
```

Když pošlete celý dokument, server odpoví `metadata.metadata: Unknown field`
a **metadata draftu vyprázdní**. Request přitom skončí s kódem 0, takže si
toho všimnete jen v `errors`.

Výměna obsahu souboru se dělá smazáním a novým nahráním; `files update`
mění pouze metadata souboru:

```bash
nrp-cmd files delete <ID> dummy.txt --repository catch-all --draft
nrp-cmd files upload <ID> ./dummy.txt '{"title": "…"}' --repository catch-all --draft
```

Smazání draftu vyžaduje `--draft`, jinak nástroj hledá publikovaný záznam
a vrátí `404 The persistent identifier is not registered`:

```bash
nrp-cmd delete record <ID> --repository catch-all --draft
```

## 8. Publikace

Draft je do publikace privátní a má `expires_at`, takže po nějaké době zmizí sám.

Publikace neprobíhá přes `links.publish` — u workflow `individual` se zakládá
požadavek typu `publish_draft`. Jeho absence v `links` tedy není závada;
publikované záznamy ho nemají také. Jaké požadavky lze na záznam podat:

```bash
curl -s -H "Authorization: Bearer <TOKEN>" \
  "https://datarepo.eosc.cz/api/requests/applicable?topic=record:<ID>" | jq .
```

Publikace registruje DOI a zveřejní záznam, takže je nevratná.

## Známé potíže

**`403 Permission denied` při zakládání záznamu.** Token je z jiné instance,
viz krok 2.

**`400 Invalid value <hodnota>`.** Slovníkové ID neodpovídá slovníku instance.
Hlásí se po jedné hodnotě.

**Warning `The parameter --log-stacktrace is used more than once`.** Chyba
v `nrp-cmd` 0.9.0, přepínač je zaregistrovaný dvakrát. Zaplaví stderr, ale
nemá vliv na funkci. Cílené potlačení, které ostatní varování nechá projít:

```bash
nrp-cmd() {
  PYTHONWARNINGS='ignore:The parameter --log-stacktrace is used more than once:UserWarning' \
    command nrp-cmd "$@"
}
```

**`metadata.locations.features[].geometry` se zahazuje.** GeoJSON geometrie
se uloží jako prázdný objekt, nebo z odpovědi zmizí úplně; `place` přežije.
Chyba je v `oarepo-model`: datový typ `dynamic-object` staví marshmallow
schéma `PermissiveSchema` s `unknown = INCLUDE` a nulou deklarovaných polí
(`src/oarepo_model/datatypes/collections.py`). `INCLUDE` ovlivňuje v marshmallow
jen `load()`, zatímco `dump()` serializuje výhradně deklarovaná pole — obsah
se tedy při každém čtení vyprázdní. Postihuje to všechna pole typu
`dynamic-object`. Ukázkový JSON v tomto adresáři proto geometrii neobsahuje
a uvádí jen `place`.
