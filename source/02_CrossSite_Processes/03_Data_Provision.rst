.. _csp-data-provision-reference-label:

Data Provision
~~~~~~~~~~~~~~

Who performs the access to the data? 
************************************
* Gateway for external requests 
* Internal users
* Workflow / business process engine

**To be specified:**

* Access of Data Collector Service? 

In which format is the data provided? 
*************************************
* AQL query result set: XML, JSON or CSV
* CDAs only if required by NSG
* Also HL7 FHIR Resources
* XDS documents:
	* IDs
	* Document direct (PDF; DICOM, XML, JSON)
* DataMart table-oriented (CSV, transmart)

How is the data transferred? 
****************************
Patient-related data: Exchange of documents and images cross-site is use case dependent:

* XCDR 
* XCA
* Internal XDS

**To be specified:**

* Data aggregated across patients?
* FHIR Task Resource ?