# Lab Orders Workflow Implementation

## iSantePlus and OpenELIS Integration

### Lab Workflow Mapping
![STU3 Diagnostics Module](http://hl7.org/fhir/STU3/diagnostic-module-resources.png)

STU3:  
http://hl7.org/fhir/STU3/diagnostics-module.html 

R4:  
http://hl7.org/fhir/diagnostics-module.html

--- 

**Example Workflow**  
https://www.hl7.org/fhir/workflow-communications.html#12.6.2.1

**Required Resources**
- `ProcedureRequest`: https://github.com/openmrs/openmrs-module-fhir/blob/master/api/src/main/java/org/openmrs/module/fhir/api/ProcedureRequestService.java
- `DiagnosticReport`: https://github.com/openmrs/openmrs-module-fhir/tree/master/api/src/main/java/org/openmrs/module/fhir/api/diagnosticreport
- `Specimen`: http://hl7.org/fhir/STU3/specimen.html (no OpenMRS implementation)
- `Sequence`: http://hl7.org/fhir/STU3/sequence.html (no OpenMRS implementation)
- `ImagingStudy`: (no OpenMRS implementation)
- `ImagingManifest`: (no OpenMRS implementation)

Required by Workflow: 
- `Task`: https://www.hl7.org/fhir/task.html (no OpenMRS Implementation)


### The `Task` resource**  
STU3: https://www.hl7.org/fhir/STU3/task.html  
R4: https://www.hl7.org/fhir/task.html

> "...describes an activity that can be performed and tracks the state of completion of that activity. It is a representation that an activity should be or has been initiated, and eventually, represents the successful or unsuccessful completion of that activity."

In our workflow, the `Task` resource can keep track of the status of the **Lab Order** made in *iSantePlus*. The `Task` resource keeps track of inputs, outputs, and task status. The status represented by a given state in the following state machine: 

![STU3-Task-State-Machine](http://hl7.org/fhir/STU3/task-state-machine.svg)

Our workflow:
1. A lab order is created in *iSantePlus*: 

2. This lab order is mapped to a `ProcedureRequest` FHIR resource:

3. A `Task` resource is created with the and linked to the `ProcedureRequest` resource:
      - `Task.basedOn` --> `ProcedureRequest`
      - `Task.status` --> `draft` 
      - `Task.businessStatus` --> ??
      - `Task.statusReason` --> ??
      - `Task.code` --> ?? (Do we want some information about this task in the Task resource, or all in the ProcedureRequest resource?)

4. Options:
      - *OpenMRS* sends a request to *OpenELIS* with the created `Task` resource?
      - *OpenMRS* notifies *OpenELIS* about the creation of the `Task` resource, which then triggers a request from *OpenELIS* to retrieve the Task resource?

      - `Task.status` --> `recieved` 



5. *OpenELIS* validates the `ProcedureRequest` and either accepts or rejects the `Task`:
      - Send an `PUT` request to OpenMRS:  `Task.status` --> `accepted` | `rejected` ??
      - Notify OpenMRS in some other fashion??

6. *OpenELIS* manages the lab order workflow, and updates the `Task.status` and optionally the `Task.businessStatus` and `Task.statusReason` with additional information about the status Lab order. 

7. When results are avialable, *OpenELIS* creates a `DiagnosticReport` resource with associated `Observations`/other resources. 
      - *OpenELIS* sends a `PUT` request to *OpenMRS* to update the `Task` resource

      - `Task.status` --> `completed`
      - `Task.output.value[1]` --> `DiagnosticReport`


**Workflow Patterns**  
http://hl7.org/fhir/STU3/workflow-communications.html#commpatternslist

**Changes in R4**
![R4 Diagnostics Module](http://hl7.org/fhir/diagnostic-module-resources.png)

- `ProcedureRequest` --> `ServiceRequest`
- No `ImagingManifest` Resource
- `Media` Resource added

https://docs.google.com/document/d/1FEx8KUpxQfRP_TRtvAZvjTSt9BiB-nX4r9Qj-jvn528/edit
