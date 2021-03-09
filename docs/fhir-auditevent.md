

# FHIR AuditEvent Resource

AuditEvent is one of the resources defined by the HL7 FHIR standard in the Security and Privacy module. It supports the requirement for FHIR servers to maintain complete tamper-proof logs of all API accesses as well as other events related to security and privacy.

## AuditEvent Model

An AuditEvent resource model allows you to record an _agent_ that performs the auditable action, an _entity_ that is the object of such action, and various details about the action and its outcome. 

This section briefly describes most important properties of AuditEvent resources. Please refer to the [standard specification](https://www.hl7.org/fhir/auditevent.html) for additional details and formal definitions.

Each AuditEvent resource must contain the following main elements (properties):

- Event type identifier `type`, chosen from the list of standard codes. The list can be extended if required.
- Event recording timestamp `recorded` in the format compatible with ISO 8601, including the timezone information.
- One or more `agent` elements, each identifying a subject that caused the event. Each `agent` is a complex element with properties that help define the agent type, role, location, applicable authorization policies etc.
- An element `source` that identifies the observer that detected the event.

AuditEvent can contain zero or more `entity` elements, each identifying the data or objects upon which the action was performed. The `action` code itself is also optional, which allows recording of events not related to particular objects, such as an account logoff. Events related to access to PHI, obviously, should contain at least one `entity` that describes the information accessed.

An `entity` must contain either the object `name` or a `query` used to access it, but not both.

## FHIR Resource Serialization Format

FHIR resources are most commonly serialized as JSON, although the standard allows other formats, including XML. Developers may choose to use other formats, such as Avro, when persistently storing audit event records for performance and storage efficiency, provided that all event properties have data types and formats as prescribed by the standard and are retained without modification. 

Examples in this guide use the JSON format.

An example of AuditEvent JSON serialization can be found [here](https://www.hl7.org/fhir/auditevent-example.json.html).

