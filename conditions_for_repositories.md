# Conditions for Creating and Modifying Repositories in the NRP

*Source: [Conditions for Creating New and Modifying Existing Domain Repositories in the National Repository Platform (v3.4)](https://docs.nrp.eosc.cz/en/docs/repo_admins/operating-repositories-in-the-nrp/conditions-for-creating-repositories)*

## 1. Establishing a repository using the standard repository systems
*Responsibilities of the user group establishing the repository*
1. Establish the role of repository administrator.
1. Establish the role of data curator.
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

## 2. Establishing a Repository Operated on NRP Resources Without Using Core Repository Systems

**The NRP provides:** the environment for data storage and running applications (S3 + Kubernetes), documentation and consultations.

**The repository administrator must ensure everything from case 1 and in addition:**

1. All items from the administrator's responsibilities when using the core systems (see chapter 1 above).
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

## 3. Integration of an Existing Independently Operated Repository into the NRP

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
