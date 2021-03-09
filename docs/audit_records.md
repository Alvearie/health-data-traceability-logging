# Audit Record Formats

There is no single commonly used standard to represent audit records pertaining
to access to health records containing PHI. 

One such format was standardized by [DMTF](https://www.dmtf.org/about) (formerly known as the Distributed
Management Task Force), an industry organization aiming to improve the interoperable
management of information technologies. It was published in 2014 as [CADF](https://www.dmtf.org/standards/cadf) -- 
Cloud Auditing Data Federation standard. It defines not only the event representation
format, but an entire event model that supports recording and auditing of security
events in cloud environments. A more detailed discussion of the CADF standard is
presented in the [corresponding section](cadf.md).

Another standardized format is described by the [HL7](glossary.md/#hl7) [FHIR](glossary.md/#fhir) specification: the [AuditEvent resource]((https://www.hl7.org/fhir/auditevent.html)). This format is described [here](fhir-auditevent.md).

Developers can choose one of these formats, taking into account overall architecture of the application and potential use cases. For example, an application that already implements support for other FHIR resources will likely benefit from using the AuditEvent record format for consistency. On the other hand, if the application is being deployed on a platform whose components already use CADF as the common audit event format, such as IBM Cloud, CADF would be a better choice. 

AuditEvent model defines fewer mandatory attribute and is therefore slightly more flexible. Note, however, that events logged with fewer details are less useful for the intended purposes of detecting and reporting improper access to sensitive information and as such may not fully address regulatory requirements.

Regardless of the chosen format it is important to strictly follow the corresponding standard when recording events; this will guarantee that the event records can be transferred to and queried by any compliant application, ensuring reliable access to the audit logs now and in the future.
