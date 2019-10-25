# SEDISH
https://github.com/sedish

## OpenHI
https://wiki.ohie.org/display/documents/OpenHIE+Introduction        E

![OpenHIE Architecture](sedish-arch.png)

## SHR
- https://wiki.ohie.org/pages/viewpage.action?pageId=19464697
- https://github.com/jembi/openshr

- https://github.com/SEDISH/oshr
- https://github.com/SEDISH/openmrs-module-shr-cdahandler

- https://github.com/jembi/hearth


**SHR Level 1 - (at least one content profile + query for existing data)**

A **phase 1** OpenHIE SHR must implement the following:

- XDS.b's provide and register document, stored query and retrieve document transactions
- At least one of the Patient Care Coordination CDA content profiles which profile the CDA Continuity of Care Document (CCD) specification.
- The Query for Existing Data (QED) profile

**SHR Level 2 - (all PCC content profiles + query for existing data + referrals)**

A **phase 2** OpenHIE SHR must implement the following:

- XDS.b's provide and register document, stored query and retrieve document transactions
- ALL of the Patient Care Coordination CDA content profiles which profile the CDA Continuity of Care Document (CCD) specification.
- The Emergency Department Referral (EDR) PCC profile which supports referrals
- The Query for Existing Data (QED) profile

**SHR Level 3 - (clinical documents + query for existing data + referrals + some form of data export - [perhaps lab and drug profiles])**

A **phase 3** OpenHIE SHR must implement the following:

- XDS.b's provide and register document, stored query and retrieve document transactions
- ALL of the Patient Care Coordination CDA content profiles which profile the CDA Continuity of Care Document (CCD) specification.
- The Emergency Department Referral (EDR) PCC profile which supports referrals
- The Query for Existing Data (QED) profile
- A to-be-determined mechanism to export data for reporting purposes

## MPI / Client Registry
https://wiki.ohie.org/display/SUB/Client+Registry+Community

## DHIS2
https://github.com/SEDISH/ohie-fr
https://wiki.ohie.org/display/SUB/Facility+Registry+Community


## Interoperability Layer