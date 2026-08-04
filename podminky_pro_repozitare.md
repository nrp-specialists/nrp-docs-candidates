# Podmínky pro vytváření a úpravu repozitářů v NRP

*Zdroj: [Conditions for Creating New and Modifying Existing Domain Repositories in the National Repository Platform (v3.4)](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)*

## 1. Založení repozitáře s využitím standardních repozitářových systémů
*Odpovědnosti uživatelské skupiny zřizující repozitář*
1. Zřídit roli správce repozitáře – partner infrastrukturního operátora, odpovědnost za data a nastavení, informován o provozních událostech, spolupráce s kyberbezpečnostním týmem.
1. Zřídit roli datového kurátora – pravidla pro ukládaná data, rozhodování o konkrétních datasetech, harmonizace metadat, interoperabilita s NMA.
1. Definovat oborové metadatové profily (ve spolupráci s IPs CARDS a specialisty). Pro složitější modely zajistit kapacitu pro implementaci na vlastní straně.
1. Definovat prvky metadatového schématu exportované do NMA (mapování na CCMM).
1. Určit seznam licencí dostupných v procesu ukládání dat.
1. Přiřadit metadatům záznamů dostatečně permisivní licenci (ekvivalent CC0).
1. Určit seznam podporovaných datových formátů (může být i "jakýkoli").
1. Definovat workflow pro ukládání dat (např. proces schvalování záznamů).
1. Definovat workflow pro přístup k datům (od otevřeného přístupu po schvalovací proces).
1. Definovat role uživatelských skupin (běžný vkladatel, kurátor, schvalovatel) a propojit na EOSC AAI.
1. Vytvořit uživatelskou dokumentaci repozitáře (pomocí prefabrikátů od NRP).
1. Vytvořit politiku repozitáře – kdy je záznam považován za uzavřený, jaké změny jsou přípustné, pravidla pro vkládání dat a přístup k nim, pravidla pro výmaz, dobu uložení atd.
1. Poskytovat uživatelskou podporu (L1) pro koncové uživatele.
1. Odesílat informace do Národního katalogu repozitářů (NKR) – registrace a aktualizace (ideálně automatizovaně přes OAI-PMH nebo API).

### Provozní checklist pro standardní repozitáře

*Zdroj: `Checklist_invenio.xlsx` (zatím interní dokument metodiků NRP)*

#### Fáze 1: Příprava
1. Požádat o zřízení repozitáře (kontaktní formulář).
1. Uskutečnit úvodní konzultaci s metodiky NRP.
1. Vytvořit seznam prioritizovaných požadavků na systém (MUST/SHOULD/COULD/WON'T HAVE).
1. Uskutečnit navazující konzultace s metodiky a dalšími týmy NRP.
1. [Milník] Vybrat repozitářový systém a založit záznam pro repozitář v NKR.

#### Fáze 2: Specifikace
1. Stanovit řízené slovníky používané v repozitáři (preferovaný formát: turtle .ttl).
1. Specifikovat, jaké se budou v repozitáři přiřazovat PID a jakým způsobem (defaultně tlačítko v UI pro přidělení DOI).
1. Předat ukázku dat a domluvit se na struktuře pro snadný import (preferovaně JSON).
1. Specifikovat vizuální identitu (logo, barevné schéma, název repozitáře).
1. Definovat komunity a pravidla pro zařazování uživatelů do komunit (vlastník komunity, politika členství a depozice).
1. Popsat požadavky na UI: browse, search, zobrazení záznamů, domovská stránka, správa repozitáře, depoziční formulář, stránka o repozitáři, další.
1. Uvést povinnou publicitu a acknowledgment (loga EU, MŠMT, EOSC CZ).
1. Dodat úvodní texty o repozitáři a specifikovat externí odkazy.
1. Na viditelném místě uvést doporučený formát citování repozitáře.
1. Stanovit metriky, které chce uživatelská skupina sledovat pro hodnocení repozitáře.
1. Zvolit režim repozitáře z hlediska zřizovatele; potvrdit souhlas s Provozními podmínkami repozitářů v NRP a s pravidly pro zřizování repozitářů v NRP.
1. [Milník] Odsouhlasit specifikaci s provozovatelem repozitářového systému, vč. rozdělení odpovědnosti za vývoj.

#### Fáze 3: Vývoj
1. Založit veřejný repozitář (GitHub) s kódem pro testovací/produkční instanci repozitáře.
1. Implementovat specifikované vlastnosti repozitáře: metadatové profily, řízené slovníky, workflows, skupiny/role, AAI, komunity/kolekce, UI, vizuál ad.
1. Požádat provozovatele NRP o přípravu smlouvy.
1. Připravit dostatečně velký vzorek dat pro prvotní/testovací import.
1. Odsouhlasit mockup uživatelského rozhraní.
1. Otestovat zpřístupněné prototypy repozitáře a předat zpětnou vazbu.
1. Namapovat non-CCMM a extended-CCMM profily na CCMM pro export do NMA (preferovaně XSLT).
1. Sepsat depoziční licenci.
1. Zapsat správce repozitáře a datového kurátora do NKR.
1. [Milník] Potvrdit finální prototyp.

#### Fáze 4: Zveřejnění

1. Provést uživatelské testování.
1. Podepsat smlouvu s provozovatelem NRP.
1. [Milník] Repozitář je provozovatelem NRP zpřístupněn a předán zřizovateli.
1. Informovat uživatelskou skupinu a veřejnost o spuštění repozitáře.

---

## 2. Založení repozitáře na zdrojích NRP bez využití standardních repozitářových systémů

**NRP poskytuje:** prostředí pro ukládání dat a běh aplikací (S3 + Kubernetes), dokumentaci a konzultace.

**Správce repozitáře musí zajistit vše z případu 1 a dále:**

1. Všechny položky z odpovědností správce při použití standardních systémů (viz výše kap. 1).
1. Instalace a provoz repozitáře a příslušné softwarové infrastruktury (alternativní repozitářový systém) v rámci prostředí NRP.
1. Nasazení oborových metadatových profilů a jejich registrace, harmonizace metadat, interoperabilita s NMA.
1. Výběr a implementace přidělování persistentních identifikátorů z podporovaných typů, konfigurace přidělených rozsahů.
1. Technické nastavení harvestování metadat do NMA dle požadavků NMA v souladu s CCMM.
1. Technická konfigurace workflow pro ukládání dat a řízení přístupu k datům.
1. Konfigurace technických integrací se systémy EOSC AAI, definice rolí uživatelských skupin.
1. Vytvoření uživatelské dokumentace.
1. Vytvoření dokumentace pro správu a provoz systému.
1. Poskytování uživatelské podpory na všech úrovních (L1–L3), kromě požadavků na provoz S3 + Kubernetes.
1. Zajištění nástrojů pro integraci do prostředí národní e-infrastruktury (přenos dat mezi repozitářem, úložištěm a výpočetními zdroji).
1. Konfigurace logování do centrálního logovacího systému NRP.
1. Zajištění kyberbezpečnostního dohledu (CESNET-CERTS, FTAS), penetrační testy, hlášení incidentů.
1. Soulad se standardními podmínkami služby a definice dalších podmínek ve spolupráci s NRP compliance.
1. Sběr statistických dat o provozu a využití systému.
1. Provozní monitoring.
1. Zajištění dostatečných personálních kapacit (systémoví administrátoři) pro stabilní provoz.

---

## 3. Integrace existujícího samostatně provozovaného repozitáře do NRP/NDI

**Správce má plnou odpovědnost** za provoz od hardwaru po službu repozitáře.

**Minimální požadavky pro připojení repozitáře k NRP:**

1. Poskytování metadat do NMA v souladu se základním metadatovým modelem (CCMM).
1. Odesílání informací do Národního katalogu repozitářů (NKR).
1. Připojení repozitáře k EOSC AAI.
1. Definování API pro přenos dat.
1. Přidělování PID (nemusí jít nutně o DOI).

**Další povinnosti:**

1. Dodržení všech ustanovení o správcích, rolích, nastavení licencí a dalších politikách.
1. Repozitář musí mít odpovídající infrastrukturu kybernetické bezpečnosti.
1. Alespoň základní úroveň monitoringu (kvalita provozu, sběr statistických dat).
1. Logování – nezbytné pro analýzu bezpečnostních incidentů.
1. Dostatečný soulad s právními a dalšími předpisy (dle povahy dat a provozu).
1. Správce musí zajistit funkčnost ekvivalentní té, kterou poskytuje NRP.