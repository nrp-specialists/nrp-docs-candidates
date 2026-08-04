# Conditions for Creating and Modifying Repositories in the NRP

*Source: [Conditions for Creating New and Modifying Existing Domain Repositories in the National Repository Platform (v3.4)](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)*

## 1. Establishing a repository using the standard repository systems
*Responsibilities of the user group establishing the repository*
1. Establish the role of repository administrator – partner of the infrastructure operator, responsible for the data and the settings, informed about operational events, collaborates with the cybersecurity team.
1. Establish the role of data curator – rules for the stored data, decisions on specific datasets, metadata harmonisation, interoperability with the National Metadata Directory (NMD).
1. Define the domain-specific metadata profiles (in collaboration with IPs CARDS and the specialists). For more complex models, ensure implementation capacity on your own side.
1. Define the metadata schema elements exported to the NMD (mapping to CCMM).
1. Determine the list of licences available in the data deposition process.
1. Assign a sufficiently permissive licence to record metadata (equivalent to CC0).
1. Determine the list of supported data formats (this may be "any").
1. Define the workflow for data deposition (e.g. the record approval process).
1. Define the workflow for data access (from open access to an approval process).
1. Define the roles of user groups (regular submitter, curator, approver) and link them to EOSC AAI.
1. Create user documentation for the repository (using the prefabricated materials from the NRP).
1. Create the repository policy – when a record is considered closed, what changes are permissible, rules for depositing data and accessing it, rules for deletion, retention periods, etc.
1. Provide L1 user support for end users.
1. Submit information to the National Catalogue of Repositories (NKR) – registration and updates (ideally automated via OAI-PMH or an API).

### Operational checklist for standard repositories

*Source: `Checklist_invenio.xlsx` (currently an internal document of the NRP repository specialists)*

#### Phase 1: Preparation
1. Request a repository (contact form).
1. Hold an introductory consultation with the NRP repository specialists.
1. Draw up a list of prioritised requirements for the system (MUST/SHOULD/COULD/WON'T HAVE).
1. Hold follow-up consultations with the repository specialists and other NRP teams.
1. [Milestone] Select a repository system and create a record for the repository in the NKR.

#### Phase 2: Specification
1. Determine the controlled vocabularies used in the repository (preferred format: turtle .ttl).
1. Specify which PIDs the repository will assign and how (by default a button in the UI assigns a DOI).
1. Hand over sample data and agree the structure the data must have for easy import (preferably JSON).
1. Specify the visual identity (logo, colour scheme, repository name).
1. Define the communities and the rules for assigning users to them (community owner, membership and deposition policy).
1. Describe the UI requirements: browse, search, record display, home page, repository administration, deposition form, about page, other.
1. State the required publicity and acknowledgment (EU, MŠMT, EOSC CZ logos).
1. Supply the introductory texts about the repository and specify the external links.
1. State the recommended citation format for the repository in a visible place.
1. Determine the metrics the user group wants to track in order to evaluate the repository.
1. Select the repository mode in terms of its establishing entity; confirm acceptance of the NRP Repository Terms of Service and of the rules for establishing repositories in the NRP.
1. [Milestone] Agree the specification with the repository system operator, including the division of responsibility for development.

#### Phase 3: Development
1. Create a public repository (GitHub) with the code for the test/production repository instance.
1. Implement the specified repository features: metadata profiles, controlled vocabularies, workflows, groups/roles, AAI, communities/collections, UI, visual design, etc.
1. Ask the NRP operator to prepare a contract.
1. Prepare a sufficiently large data sample for the initial/test import.
1. Accept the user interface mockup.
1. Test the released repository prototypes and give feedback.
1. Map non-CCMM and extended-CCMM profiles to CCMM for export to the NMD (preferably XSLT).
1. Write the deposition licence.
1. Record the repository administrator and the data curator in the NKR.
1. [Milestone] Confirm the final prototype.

#### Phase 4: Going live

1. Carry out user testing.
1. Sign the contract with the NRP operator.
1. [Milestone] The NRP operator makes the repository available and hands it over to the establishing entity.
1. Inform the user group and the public about the launch of the repository.

---

## 2. Establishing a repository on NRP resources without the standard repository systems

**The NRP provides:** the environment for data storage and running applications (S3 + Kubernetes), documentation and consultations.

**The repository administrator must ensure everything from case 1 and in addition:**

1. All items from the administrator's responsibilities when using the standard systems (see chapter 1 above).
1. Installation and operation of the repository and the corresponding software infrastructure (an alternative repository system) within the NRP environment.
1. Deployment of domain-specific metadata profiles and their registration, metadata harmonisation, interoperability with the NMD.
1. Selection and implementation of persistent identifier assignment from the supported types, configuration of the assigned ranges.
1. Technical setup of metadata harvesting into the NMD according to NMD requirements, in compliance with CCMM.
1. Technical configuration of the workflow for data deposition and access control to the data.
1. Configuration of technical integrations with the EOSC AAI systems, definition of user group roles.
1. Creation of user documentation.
1. Creation of documentation for system administration and operation.
1. Provision of user support at all levels (L1–L3), except for requests concerning the operation of S3 + Kubernetes.
1. Provision of tools for integration into the national e-infrastructure environment (transfer of data between the repository, storage and computational resources).
1. Configuration of logging into the NRP central logging system.
1. Provision of cybersecurity oversight (CESNET-CERTS, FTAS), penetration tests, incident reporting.
1. Compliance with the standard service conditions and definition of further conditions in cooperation with NRP compliance.
1. Collection of statistical data on the operation and usage of the system.
1. Operational monitoring.
1. Provision of sufficient personnel capacity (system administrators) for stable operation.

---

## 3. Integration of an existing independently operated repository into the NRP/NDI

**The administrator bears full responsibility** for operation, from hardware to the repository service itself.

**Minimum requirements for connecting a repository to the NRP:**

1. Providing metadata to the NMD in accordance with the core metadata model (CCMM).
1. Submitting information to the National Catalogue of Repositories (NKR).
1. Connecting the repository to EOSC AAI.
1. Defining APIs for data transfer.
1. Assigning PIDs (not necessarily DOIs).

**Further obligations:**

1. Compliance with all provisions on administrators, roles, licence settings and other policies.
1. The repository must have an appropriate cybersecurity infrastructure.
1. At least a basic level of monitoring (operational quality, collection of statistical data).
1. Logging – essential for analysing security incidents.
1. Sufficient compliance with legal and other regulations (depending on the nature of the data and the operation).
1. The administrator must ensure functionality equivalent to that provided by the NRP.
