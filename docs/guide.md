# Logging Access to Protected Health Information

Organizations regulated by [HIPAA](glossary.md#hipaa) and similar legislation are required to ensure 
that Protected Health Information (PHI) is stored and handled in a secure manner. In 
particular, HIPAA mandates that such organizations must implement "policies and 
procedures to prevent, detect, contain, and correct security violations". As part
of this requirement organizations must put in place "procedures to regularly review records 
of information system activity, such as audit logs, access reports, and security 
incident tracking reports" (HIPAA § 164.30).

Technical safeguards (§ 164.312) must include "hardware, software, and/or procedural mechanisms that record and examine activity in information systems that contain or use electronic protected health information."

This guide describes how developers of healthcare applications and other software
that is used to process and store PHI can support these security requirements by
recording access to PHI, storing and reporting on these records. 

## When to Log Auditable Events

According to HIPAA, "_access_ means the ability or the means necessary to read, write, modify, or communicate data/information or otherwise use any system resource". As a result, a software application that performs any of these actions upon PHI must record them, including what PHI was accessed, when, and by whom (what process or person), and store these records securely.

For the definition of PHI, please refer to [this section](phi.md).

In some cases infrastructure components, such as databases, messaging services, API proxies, and managed services of cloud providers are capable of generating logs that can potentially address HIPAA requirements pertaining to PHI access. However, they rarely have an ability to determine what information constitutes PHI; as a result, volumes of log records they generate are unnecessarily large as they often include records of access to _any_ information. In addition, the format of such log records is not standardized and does not facilitate querying and reviewing them for HIPAA compliance.

It is the responsibility of developers to equip their applications with a means of logging access to PHI. When choosing the event record format, consider using one of the standards described [here](audit_records.md); generating audit event records in a standardized format improves interoperability of your application and helps to develop a more flexible architecture by allowing the use of existing standard-compliant components in place of custom-created ones.

It is a critical error if the application is unable to create or send an access event record; in such cases access to PHI should not be allowed to proceed. For this reason applications should use the "write ahead" approach and generate and send the audit event record _before_ actually allowing access to PHI.

## Sensitive Data in Audit Log Records

Records of access to PHI do not need to, and should not themselves contain PHI. You can minimize the risk of PHI and other protected information exposure in audit log records by not including actual medical record numbers (MRN), patient IDs, or [other personally identifying information](#phi) (PII), and using instead surrogate (synthetic) identifiers. While such surrogate identifiers can be mapped to their source records when generating audit reports, they don't constitute PHI by themselves and do not expose PII directly in the logs.

Synthetic identifiers must not be derived from or otherwise related to any actual PII. They also must not be used for any other purpose apart from identifying records inside the particular application; for example, they must not be used when exchanging data with other applications or externals systems.

The application must internally maintain the mapping between such surrogate identifiers and the 
actual record identifiers, to be used for HIPAA reporting purposes.

## Persistent Storage of Audit Records

When persistently storing logged audit events developers can choose formats other than the standardized formats used for transporting event records. For example, they may decide to decompose CADF event records for storing them in relational database tables, or save records in Parquet files for efficient storage and querying. However, they need to ensure that the record element data types and formats remain compatible with the chosen standard and the values remain unchanged. This will allow them when necessary to reconstruct the records in their original format to maintain the application interoperability.

## Reporting and Alerts

Typical reports for auditing the PHI access control compliance might answer the questions like "Who/what entities had access to any PHI within the given time interval", "Who had access to a specific PHI item during the entire log interval", "What PHI items have been accessed during the during the particular user session", "Was there any PHI access outside business hours in the past week", etc. 

Note that compliance reports like this themselves are subject to privacy regulations; they must be retained, and access to them controlled, according to such regulations. For example, HIPAA stipulates that organizations subject to its rules "must maintain, until six years after the later of the date of their creation or last effective date, its privacy policies and procedures, its privacy practices notices, disposition of complaints, and other actions, activities, and designations that the Privacy Rule requires to be documented," which applies in particular to the audit activity records.

Developers can choose any tools available for reporting on the chosen storage solution, with the condition that it offers the necessary means of user authentication, authorization, and secure retention and disposal of audit reports. 

Application developers should consider implementing an alert mechanism, based on the auditable event, to send notifications and initiate response in case of unexpected occurrences of PHI access. Rules for such notifications will be application-specific; depending on the expected workload patterns they could include access to PHI outside the normal business hours; access to multiple PHI records inside a single user session; requests origination from unexpected locations; etc. Alert rules can be applied to the event records in motion, as they are being sent, for immediate reaction, or to data at rest after they have been persistently stored, which could allow more intelligent analysis and detection of unusual access patterns.

## Security 

Auditable event records must be protected from unauthorized access and modification while in transit ("in motion") and after they are persistently stored ("at rest"). 

Transport security is achieved by encrypting the communication channels used to move records from their sources to the storage location and requiring reliable authentication at the channel endpoints. 

Storage security also involves encrypting saved records using the methods appropriate for the chosen storage medium (database table encryption, entire disk encryption). It also requires strict authentication; only persons responsible for enforcing regulatory controls and conducting audits should be able to read the event logs, and no-one should be able to alter recorded events.

When the logs are no longer needed they should be destroyed, along with any archive copies, using a method that prevents data recovery. In deployments where you do not have access to the storage media, such as when using managed database or storage services, cryptographic destruction (destruction of data encryption keys) is appropriate, as it renders encrypted data nonrecoverable.

## Availability

It is important to ensure that audit event records are not lost or damaged, neither in transit nor in storage, to maintain regulatory compliance. Choose a reliable transport with "at least once" or "exactly once" semantics, such as Apache Kafka or similar messaging service. (It is OK to have duplicate records of an event, but it is never acceptable to miss an event.) 

Event records in persistent storage must be backed up regularly to an off-site location to guarantee that access to the audit logs is possible even in case of storage failure or site-wide outage. The application disaster recovery plans should include the infrastructure used to collect, transport, and store audit event logs.
