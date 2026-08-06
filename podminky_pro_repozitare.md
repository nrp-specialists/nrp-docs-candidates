# Podmínky pro vytváření a úpravu repozitářů v NRP

*Zdroj: [Conditions for Creating New and Modifying Existing Domain Repositories in the National Repository Platform (v3.4)](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)*

## 1. Založení repozitáře s využitím standardních repozitářových systémů

*Odpovědnosti uživatelské skupiny zřizující repozitář*
1. Zřídit roli správce repozitáře.
1. Zřídit roli datového kurátora.
1. Definovat oborové metadatové profily. Pro složitější modely zajistit kapacitu pro implementaci na vlastní straně.
1. Definovat prvky metadatového schématu exportované do NMA (mapování na CCMM).
1. Určit seznam licencí dostupných v procesu ukládání dat.
1. Přiřadit metadatům záznamů dostatečně permisivní licenci (ekvivalent CC0).
1. Určit seznam podporovaných datových formátů (může být i "jakýkoli").
1. Definovat workflow pro ukládání dat (např. proces schvalování záznamů).
1. Definovat workflow pro přístup k datům (od otevřeného přístupu po schvalovací proces).
1. Definovat role uživatelských skupin (běžný vkladatel, kurátor, schvalovatel) a propojit s EOSC AAI.
1. Vytvořit uživatelskou dokumentaci repozitáře (s využitím připravených materiálů NRP).
1. Vytvořit politiku repozitáře.
1. Poskytovat uživatelskou podporu (L1) pro koncové uživatele.
1. Odesílat informace do Národního katalogu repozitářů (NKR).

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

## 3. Integrace existujícího samostatně provozovaného repozitáře do NRP

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