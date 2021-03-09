# Health Data Traceability and Logging - HDTL

This project introduces a framework for healthcare applications to address
regulatory requirements related to collecting, retaining, protecting, and monitoring
 logs of access to [Protected Health Information](docs/phi.md) (PHI).

Health Insurance Portability and Accountability (HIPAA) in the USA and similar
regulations in other countries require that all organizations that create or process
health information maintain privacy and security of such information. As part of this requirement
these organization must implement controls such as the following:
- Collect logs recording system, network, and software activity, including 
  logs of access to PHI by application processes and users.
- Protect such logs from unauthorized access and modification.
- Retain the logs for the period prescribed by the regulations or, if not prescribed,
  for the period appropriate for the purpose.
- Provide means of monitoring the logs and generating evidence reports.

This framework can also be applied for logging of other critical or sensitive information, required for regulatory compliance, in support of data quality, fidelity, lineage, and similar.  

It is _not_ pertinent to regular application logging for operational support and troubleshooting; for that applications should use standard logging mechanisms and frameworks available for their deployment platforms.

Additional information on what constitutes PHI can be found [here](docs/phi.md).

General guidance and requirements for logging access to PHI is [here](docs/guide.md).

Discussion of the formats appropriate for PHI audit logs is [here](docs/audit_records.md).

Architecture of a sample system supporting the PHI access logging requirements is shown [here](docs/sample_arch.md).
