# Recommended Procedure for Creating Repositories in the NRP

## 1. Establishing a repository using the standard repository systems
*Responsibilities of the user group establishing the repository, roughly divided by the phases of building the repository*

| # | Task | Docs/Action |
| --- | --- | --- |
| **1.1** | **PREPARATION** | |
| 1.1.1 | Request a repository | send request [CZ](https://www.eosc.cz/sluzby/ukladani/repozitare-v-nrp/zalozeni-repozitare-v-nrp) \| [EN](https://www.eosc.cz/en/services/data-storage/repositories-in-nrp/creating-repositories-in-the-nrp)|
| 1.1.2 | Introductory consultation with the NRP repository specialists | outline [CZ/EN](https://researchinfracz.sharepoint.com/:w:/s/NRP/IQB7Q4Aa4FXBQqIRDzMzrTB8AVvfrzZ_-uTDuOYBTd3VriQ?e=dZgIxY) |
| 1.1.3 | List of prioritised requirements for a repository | template [EN](https://researchinfracz.sharepoint.com/:x:/s/NRP/IQAdSySSl_F8SqNlLayfHxVcAeS_ia9ha84DjckegRkb-yI?e=C6PSq6) |
| 1.1.4 | Follow-up consultations with the repository specialists and other NRP teams | |
| 1.1.5 | **Milestone:** Select a repository system and create a record for the repository in the NCR. | |
| **1.2** | **SPECIFICATION** | |
| 1.2.1 | Define the domain-specific metadata profiles; for more complex models, secure implementation capacity on your own side | docs [EN](https://nrp-cz.github.io/docs/customize/model_backend/model) |
| 1.2.2 | Define the metadata schema elements exported to the NMD (mapping to CCMM) | |
| 1.2.3 | Determine the controlled vocabularies used in the repository | |
| 1.2.4 | Define the workflows for data deposition and for data access | docs [CESNET Invenio](https://nrp-cz.github.io/docs/customize/workflows) |
| 1.2.5 | Define the roles of user groups (regular submitter, curator, approver) and the communities if applicable, and link them to EOSC AAI | docs [CESNET Invenio](https://nrp-cz.github.io/docs/administration/communities) |
| 1.2.6 | Specify which PIDs the repository will assign and how (by default a button in the UI assigns a DOI) | 1. see [identifikatory.cz](https://identifikatory.cz/)<br />2. docs [CESNET Invenio](https://nrp-cz.github.io/docs/customize/oarepo_doi) |
| 1.2.7 | Describe the UI requirements: browse, search, record display, home page, deposition form, etc. | |
| 1.2.8 | Determine the list of licences available in the data deposition process; assign a sufficiently permissive licence to the metadata | |
| 1.2.9 | Determine the list of supported data formats (this may be "any") | |
| 1.2.10 | Hand over sample data and agree the structure the data must have for easy import (preferably JSON) | |
| 1.2.11 | Specify the visual identity (logo, colour scheme, repository name), including the required publicity and acknowledgment (EU, MŠMT, EOSC CZ logos) | |
| 1.2.12 | Select the repository mode in terms of its establishing entity; confirm acceptance of the NRP Terms of Service and of the Rules for Establishing Repositories in the NRP | 1. NRP Terms of Service [CZ](https://www.eosc.cz/media/4130969/p1_pp_repozitare_nrp.pdf) <br />2. Rules for Establishing Repositories in the NRP [EN](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)|
| 1.2.13 | Determine the metrics the user group wants to track in order to evaluate the repository | |
| 1.2.14 | **Milestone:** Agree the specification with the repository system operator, including the division of responsibility for development. | |
| **1.3** | **DEVELOPMENT** | |
| 1.3.1 | Implement the specified repository features: metadata profiles, controlled vocabularies, workflows, groups/roles, AAI, communities/collections, UI, visual design, etc. | |
| 1.3.2 | Create a public repository (GitHub) with the code for the test/production repository instance | |
| 1.3.3 | Ask the NRP operator to prepare a contract | via repository specialists |
| 1.3.4 | Prepare a sufficiently large data sample for the initial/test import | |
| 1.3.5 | Create the introductory texts about the repository and specify the links to external resources | |
| 1.3.6 | State the recommended citation format for the repository in a visible place | |
| 1.3.7 | Accept the user interface mockup | |
| 1.3.8 | Test the released repository prototypes and give feedback | |
| 1.3.9 | Write the repository policy and the deposition licence | EOSC CZ sample deposition licences [CZ/EN](https://www.eosc.cz/en/projects/outcomes-of-the-eosc-cz-initiative#depo_licences) |
| 1.3.10 | Establish the role of repository administrator and record it in the NCR | |
| 1.3.11 | Establish the role of data curator and record it in the NCR | |
| 1.3.12 | Create user documentation for the repository | |
| 1.3.13 | **Milestone:** Confirm the final repository prototype. | |
| **1.4** | **GOING LIVE** | |
| 1.4.1 | Carry out user testing | |
| 1.4.2 | Sign the contract with the NRP operator and update the repository record in the NCR | |
| 1.4.3 | Provide L1 user support for end users | |
| 1.4.4 | **Milestone:** The NRP operator makes the repository available and hands it over to the establishing entity. | |
