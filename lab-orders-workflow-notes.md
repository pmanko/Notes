
- [SEDISH Setup](#sedish-setup)
  - [Docker Demo Env](#docker-demo-env)
- [iSantePlus Setup](#isanteplus-setup)
  - [Additional OpenMRS Modules in iSantePlus](#additional-openmrs-modules-in-isanteplus)
  - [Database Dump](#database-dump)
  - [Module Dump](#module-dump)
  - [SDK Setup](#sdk-setup)
  - [Docker Setup](#docker-setup)
- [FHIR Module Version Upgrade](#fhir-module-version-upgrade)
- [Sync 2.0](#sync-20)
- [](#)
  - [OpenMRS Support Overview](#openmrs-support-overview)

# SEDISH Setup
https://github.com/SEDISH

## Docker Demo Env
https://github.com/SEDISH/demo-environment

# iSantePlus Setup
https://github.com/isanteplus

iSantePlus runs on the OpenMRS Ref App 2.5 distribution, and includes some modules on top of this distribution to meet the specific requirements for the software.


## Additional OpenMRS Modules in iSantePlus
- [Main iSantePlus Module](https://github.com/IsantePlus/openmrs-module-isanteplus)
- [iSantePlus Report Module](https://github.com/IsantePlus/openmrs-module-isanteplusreports)
- [Address Hierarchy Module](https://github.com/openmrs/openmrs-module-addresshierarchy)
- [Extended Internationalization Support Module](https://github.com/openmrs/openmrs-module-exti18n)
- [Haiti Core Module](https://github.com/openmrs/openmrs-module-haiticore)
- [XDS Sender Module](https://github.com/IsantePlus/openmrs-module-xds-sender)

## Database Dump
https://bintray.com/isanteplus/clean-database/download_file?file_path=Dump20190331.sql.zip

## Module Dump
https://bintray.com/isanteplus/clean-database/download_file?file_path=modules.zip

## SDK Setup
https://wiki.openmrs.org/display/docs/OpenMRS+SDK#OpenMRSSDK-Distributions
https://github.com/IsantePlus/openmrs-distro-isanteplus

`mvn openmrs-sdk:setup -DserverId=isanteplus-dev -Ddistro=referenceapplication:2.5 -DdbUri=jdbc:mysql://localhost:3306/isanteplus-dev -DdbUser=isante -DdbPassword=isante` 

In each module repo folder that you want to develop on and deploy to the server, run the following:
`mvn openmrs-sdk:deploy -DserverId=isanteplus-dev`

## Docker Setup
https://github.com/IsantePlus/isanteplus-docker


# FHIR Module Version Upgrade
https://hapifhir.io/download.html

R4 is supported starting in V3.7.0. Currently, the FHIR Module is using HAPI FHIR Base V2.5.

An upgrade to R4 would require:
- upgrading HapiFhirBaseVersion >= 3.7: https://github.com/openmrs/openmrs-module-fhir/blob/1.19.0/pom.xml#L73
- Replacing `hapi-fhir-structures-dstu3` with `hapi-fhir-structures-r4`: https://github.com/openmrs/openmrs-module-fhir/blob/baee2bacfc8ed96f99ab6067320b1d7b44179e74/pom.xml#L154
- Replacing `hapi-fhir-validation-resources-dstu3` with `hapi-fhir-validation-resources-r4`

**Upgrade Commits**

HAPI:  
- https://github.com/openmrs/openmrs-module-fhir/pull/121/commits/f82fb92c5e480d1e8165a4626c764cd8d9ab4995
- https://github.com/openmrs/openmrs-module-fhir/pull/122/commits/00edc1e56596883dd8a9f10401ff2faf695d53f7

HAPI:  
https://github.com/openmrs/openmrs-module-fhir/pull/131/commits/4fc831fd2fc35b323d2956a494cab7a1c041850c

DSTU3:  
https://github.com/openmrs/openmrs-module-fhir/pull/132/commits/d7c6a26a1873bd6bfcc5fdc54862ad01243ca3c6

HAPI:  
https://github.com/openmrs/openmrs-module-fhir/pull/155

HAPI?:  
https://github.com/openmrs/openmrs-module-fhir/pull/213


# Sync 2.0
https://github.com/openmrs/openmrs-module-fhir/pull/142/commits/d6784cbd1a70efec2b412ab3b2d8abc099e9b686

# 
## OpenMRS Support Overview
https://docs.google.com/spreadsheets/d/13WF0Vv9wU7_JFDYFlDQh7vJwd6kJnm98eUtFvV5NuZg/edit#gid=0
