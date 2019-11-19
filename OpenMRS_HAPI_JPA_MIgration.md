- [OpenMRS and the HAPI JPA Server](#openmrs-and-the-hapi-jpa-server)
  - [Using HAPI JPA with OpenMRS](#using-hapi-jpa-with-openmrs)
  - [Development Plan](#development-plan)
  - [Work Plan Tickets](#work-plan-tickets)
  - [Links](#links)

# OpenMRS and the HAPI JPA Server 
![JPA Arch](https://hapifhir.io/images/jpa_architecture.png)

https://hapifhir.io/doc_jpa.html

## Using HAPI JPA with OpenMRS
The HAPI FHIR project has a number of different components, outlined nicely in the HAPI documentation [table of contents](https://hapifhir.io/docindex.html) Four that are important to our work are the Data Model, the RESTFul Server, the RESTful Client, and the JPA/Database Server. The current FHIR module utilizes libraries from the first three components: the [Data Model packages](https://hapifhir.io/apidocs-dstu3/index.html)  provide support for the representation of FHIR resources, the [RESTful Server packages](https://hapifhir.io/apidocs-server/index.html) are used to implement [the FHIR Server in the FHIR Module](https://github.com/openmrs/openmrs-module-fhir/blob/3d34a4475b24c42e9c90b64308b0cce0045bd4c6/omod/src/main/java/org/openmrs/module/fhir/server/FHIRRESTServer.java), and the [FHIR Module Admin Client](https://github.com/openmrs/openmrs-module-fhir/blob/3d34a4475b24c42e9c90b64308b0cce0045bd4c6/api/src/main/java/org/openmrs/module/fhir/api/util/FHIRRESTfulGenericClient.java) is implemented using the [HAPI Restful Client](https://hapifhir.io/apidocs-client/index.html). 

The [HAPI JPA Server packages](https://hapifhir.io/apidocs-jpaserver/index.html) provide additional functionality to the three components above that include the business logic and database support required to spin up a fully-functioning FHIR server. Like OpenMRS, the HAPI JPA server uses Hibernate for the object-relational mapping layer. By default, the HAPI server uses [Apache Derby](https://db.apache.org/derby/) as the database, but MySQL (and any other DB supported by Hibernate) can be easily used instead. 

Due to similar architectures and many shared dependencies, the HAPI JPA server would likely be relatively easy to integrate into the OpenMRS FHIR module. Such an integration would provide a straightforward pathway for migration from supporting FHIR resources using the OpenMRS data model, to spinning up a native, fully-functional FHIR server where resource support could be turned on using [a single setting](https://github.com/uw-fhir/hapi-fhir-jpaserver-starter/blob/c283e79b1474c1c76b629164a4c62b9af72e9a64/src/main/resources/hapi.properties#L60). 


## Development Plan

The overall plan would invovle spinning up an instance of the HAPI server alongside the FHIR server provided by OpenMRS, providing a schema for this server to use for its data model, and setting up the routing to correctly route requests to either the core OPenMRS app, the FHIR module, or the JPA Server. 

With this setup, new or existing resources could be implemented in parallel on the HAPI JPA server side, and their use transitioned to once the implementation is complete. This setup would also allow for a much more rapid enabling of new resources or other functionality defined by the FHIR spec that the current FHIR module does not support. 

## Work Plan Tickets
1. Add support for the JPA FHIR Schema in the MySQL database. (4h)
   
2. Start up a JPA server in parallel to the OpenMRS server using this schema, and route a subset of requests to this server. (1 day)

For each currently-implemented resource:
(Obs, ProcedureRequest, DiagnosticReport)

3. Connect the current RESTful server services to the JPA DOA

4. Intercept FHIR Module requests and create a parallel representation in the JPA server 

5. Migrate OpenMRS data to JPA database.
   
For each new resource:

3. Enable resource support in the properties.

4. Migrate OpenMRS data to JPA database.


## Links
- https://hapifhir.io/doc_rest_server_interceptor.html
- 
