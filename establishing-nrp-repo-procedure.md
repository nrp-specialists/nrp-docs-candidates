# Recommended Procedure for Establishing a Repository Using the Core Repository Systems
*Responsibilities of the user group establishing the repository, roughly divided by the phases of building the repository*

## Abbreviations

| Abbreviation | Meaning |
| --- | --- |
| **AAI** | Authentication and Authorisation Infrastructure — here always the EOSC AAI, the federated login the NRP repositories use |
| **CCMM** | Czech Core Metadata Model — the core metadata model that repositories map their metadata to for export to the NMD |
| **CESNET** | operator of the NRP, and developer of the CESNET Invenio repository system |
| **DOI** | Digital Object Identifier — the PID type assigned by default |
| **EOSC** | European Open Science Cloud |
| **EOSC CZ** | the Czech national initiative implementing the EOSC |
| **JSON** | JavaScript Object Notation — the preferred format for handing over sample data |
| **L1** | first-level user support, i.e. the front line answering end users' questions |
| **MŠMT** | Ministerstvo školství, mládeže a tělovýchovy — the Czech Ministry of Education, Youth and Sports |
| **NCR** | National Catalogue of Repositories (Národní katalog repozitářů, NKR) |
| **NMD** | National Metadata Directory (Národní metadatový adresář, NMA) |
| **NRP** | National Repository Platform (Národní repozitářová platforma) |
| **PID** | persistent identifier |
| **UI** | user interface |

## Procedure

| # | Task | Docs/Action |
| --- | --- | --- |
| **1.** | **PREPARATION** | |
| 1.1 | Request a repository | send request [CZ](https://www.eosc.cz/sluzby/ukladani/repozitare-v-nrp/zalozeni-repozitare-v-nrp) \| [EN](https://www.eosc.cz/en/services/data-storage/repositories-in-nrp/creating-repositories-in-the-nrp)|
| 1.2 | Hold an introductory consultation with the NRP repository specialists | outline [CZ/EN](https://researchinfracz.sharepoint.com/:w:/s/NRP/IQB7Q4Aa4FXBQqIRDzMzrTB8AVvfrzZ_-uTDuOYBTd3VriQ?e=dZgIxY) |
| 1.3 | Draw up a list of prioritised requirements for the repository | template [EN](https://researchinfracz.sharepoint.com/:x:/s/NRP/IQAdSySSl_F8SqNlLayfHxVcAeS_ia9ha84DjckegRkb-yI?e=C6PSq6) |
| 1.4 | Hold follow-up consultations with the repository specialists and other NRP teams | |
| 1.5 | **Milestone:** Select a repository system and create a record for the repository in the NCR. | |
| **2.** | **SPECIFICATION** | |
| 2.1 | Define the domain-specific metadata profiles; for more complex models, secure implementation capacity on your own side | docs [EN](https://nrp-cz.github.io/docs/customize/model_backend/model) |
| 2.2 | Define the metadata schema elements exported to the NMD (mapping to CCMM) | |
| 2.3 | Determine the controlled vocabularies used in the repository | |
| 2.4 | Define the workflows for data deposition and for data access | docs [CESNET Invenio](https://nrp-cz.github.io/docs/customize/workflows) |
| 2.5 | Define the roles of user groups (regular submitter, curator, approver) and the communities if applicable, and link them to EOSC AAI | docs [CESNET Invenio](https://nrp-cz.github.io/docs/administration/communities) |
| 2.6 | Specify which PIDs the repository will assign and how (by default a button in the UI assigns a DOI) | 1. see [identifikatory.cz](https://identifikatory.cz/)<br />2. docs [CESNET Invenio](https://nrp-cz.github.io/docs/customize/oarepo_doi) |
| 2.7 | Describe the UI requirements: browse, search, record display, home page, deposition form, etc. | |
| 2.8 | Determine the list of licences available in the data deposition process; assign a sufficiently permissive licence to the metadata | |
| 2.9 | Determine the list of supported data formats (this may be "any") | |
| 2.10 | Hand over sample data and agree the structure the data must have for easy import (preferably JSON) | |
| 2.11 | Specify the visual identity (logo, colour scheme, repository name), including the required publicity and acknowledgement (EU, MŠMT, EOSC CZ logos) | |
| 2.12 | Select the repository mode in terms of its establishing entity; confirm acceptance of the NRP Terms of Service and of the Rules for Establishing Repositories in the NRP | 1. NRP Terms of Service [CZ](https://www.eosc.cz/media/4130969/p1_pp_repozitare_nrp.pdf) <br />2. Rules for Establishing Repositories in the NRP [EN](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)|
| 2.13 | Determine the metrics the user group wants to track in order to evaluate the repository | |
| 2.14 | **Milestone:** Agree the specification with the repository system operator, including the division of responsibility for development. | |
| **3.** | **DEVELOPMENT** | |
| 3.1 | Implement the specified repository features: metadata profiles, controlled vocabularies, workflows, groups/roles, AAI, communities/collections, UI, visual design, etc. | |
| 3.2 | Create a public repository (GitHub) with the code for the test/production repository instance | |
| 3.3 | Ask the NRP operator to prepare a contract | via repository specialists |
| 3.4 | Prepare a sufficiently large data sample for the initial/test import | |
| 3.5 | Create the introductory texts about the repository and specify the links to external resources | |
| 3.6 | State the recommended citation format for the repository in a visible place | |
| 3.7 | Accept the user interface mockup | |
| 3.8 | Test the released repository prototypes and give feedback | |
| 3.9 | Write the repository policy and the deposition licence | EOSC CZ sample deposition licences [CZ/EN](https://www.eosc.cz/en/projects/outcomes-of-the-eosc-cz-initiative#depo_licences) |
| 3.10 | Establish the role of repository administrator and record it in the NCR | |
| 3.11 | Establish the role of data curator and record it in the NCR | |
| 3.12 | Create user documentation for the repository | |
| 3.13 | **Milestone:** Confirm the final repository prototype. | |
| **4.** | **GOING LIVE** | |
| 4.1 | Carry out user testing | |
| 4.2 | Sign the contract with the NRP operator and update the repository record in the NCR | |
| 4.3 | Provide L1 user support for end users | |
| 4.4 | **Milestone:** The NRP operator makes the production repository instance available and hands it over to the repository administrator. | |