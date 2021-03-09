
# CADF Resource Type Taxonomy

Taxonomy of the resource `typeURI` property values, defined by the CADF specification, is designed to standardize resource types that helps consumers to classify resources using well-defined categories. Developers can extend the taxonomy if necessary, adding new type URIs under any of the top level types ("compute", "data", "network", "security", "service", or "storage").

Most of the types are self-explanatory. Comments are added in the table below to expand acronyms and resolve ambuguity.

|Type URI| Comment|
|:----------------|:-----|
|compute/cpu 
|compute/machine
|compute/node
|compute/process
|compute/thread
|
|data/catalog
|data/config
|data/database
|data/directory
|data/file
|data/image
|data/log
|data/message
|data/message/stream
|data/module
|data/package
|data/report
|data/template
|data/workload
|data/security
|
|network/cluster
|network/connection 
|network/domain 
|network/host
|network/node 
|
|security/account
|security/account/user 
|security/account/admin 
|security/credential 
|security/group
|security/identity 
|security/key 
|security/license 
|security/node
|security/policy 
|security/profile 
|security/role 
|
|service/bss |Business Support Services
|service/bss/billing 
|service/bss/location 
|service/bss/metering 
|service/composition |Services that support the compositing of independent services into a new service offering
|service/composition/orchestration
|service/composition/workflow
|service/compute |Infrastructure services for managing computing resources.
|service/database |Managed database as a service|
|service/image  |Infrastructure services for managing virtual machine images and associated metadata.
|service/network |Infrastructure services for managing networking (fabric).
|service/oss |Operational Support Services
|service/oss/capacity
|service/oss/configuration
|service/oss/logging
|service/oss/monitoring
|service/oss/virtualization
|service/security |Security services including Identity, Policy, and Access Mgmt., Authentication, Authorization,  etc.
|service/storage
|service/storage/block
|service/storage/object
|
|storage/container 
|storage/database 
|storage/directory
|storage/memory 
|storage/node 
|storage/queue
|storage/volume
|unknown
