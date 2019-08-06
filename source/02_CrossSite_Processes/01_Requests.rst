.. _csp-requests-reference-label:

Requests
~~~~~~~~

Who has permission to submit data requests?
*******************************************
* External / internal research scientist affiliated with the HiGHmed context
* Care: Phycisian affiliated with the HiGHmed use-cases / external phycisians

**Use Cases**

* Care: clinic internal and similar patient cross-site requests (e.g., oncology use case)
* Research internal and HiGHmed cross-site
* Reseach cross-consortium

Each site has its own Use & Access Committee (UAC), there is no consortium-wide committee. There will be a site-specific approach, possibly with proposals from the National Steering Committee (NSG). HiGHmed internally it should be kept consistent. The UAC has to be envolved in every request and determines the final processes. 

External (e.g., other MII-consortium) and cross-consortium requests are planned to be implemented as Black Box, eventually as manual processes.

**To be specified:**

* The involvment of the UAC for *number of cases inquiries*. Should requests of this type always pass? Basic decision of the UAC required.

Which requests are accepted?
****************************
* Cross-patient data (e.g. number of cases)
* Requests for specified (similar) patients
* Patient-related data:
	* Structured data from openEHR incl. results from Omics-analysis
	* Structured / unstructured documents from respository
	* Non-pseudonymized data in the care context (e.g. tumor board), also cross-site if co-therapist
	* Image data
* No priority for:
	* Bio-material
	* Service requests (e.g. for special analysis)

How many requests are permitted?
********************************
In general, there are no restirctions. But, what was once rejected by the UAC should usually not be requested again, depending on the reason for the rejection. If necessary, a new request is possible if the cohort has become larger. There will be a result tracking and possible blacklisting.

Requests must go to the individual sites, as there is no consortium-wide UAC. The lead UAC takes over federation. Decisions must be made by each local UAC, there is a fast-track if the lead UAC has agreed.

How does a requesting person know what data is available? 
*********************************************************
A cohort explorer in the form of a tree representation (without counts) will be available.

* General questions can be asked: Does a site offer data type x? 
* Example Tool Birger: this tool should run at every location; with an interface for comparison with other locations. 

**To be specified:**

* Should their be a Metadata Dictionary?
* Should quality assurance be taken into account?

In wich format are the requests specified? 
******************************************
* AQL (also IDs of stored queries)
* XDS metadata or XDS-I for DICOM data (Registry Stored Query)
* Workflow / Container formats:
	* HL7 FHIR Task Resource
	* Stored Queries

**To be specified:**

* Usage of HL7 FHIR Resources as request format?
* Free-text with defined vocabulary, especially within one location?
* XDW for workflow / container format?

What tools are used to specify the requests? 
********************************************
* Request client: has to be developed for each location, which forwards the request to the UAC(s).
* Priority 1 for the tool (research):
	* Search metadata (XDS metadata and metadata repository)
	* Cohort explorer
	* Create request
	* Manage requests
* Other request tools can be:
	* Patient portal 
	* Tumorboard tool
	* ...

**To be specified:**

* Decide whether the client sends requests to multiple / all UACs or only to the local one and the request is forwarded from there. 

How are requests transmitted cross-site? 
****************************************
* HL7 FHIR Task Resources
* Possibly non-patient file sharing - NPFSm (IHE profile, based on FHIR), profiles from QRPH domain
* In the context of patient care: XDS Query / possibly cross community  

**To be specified:**

* Point to be discussed further! (Exchange with Smith)

What are expected response times?
*********************************
* UAC: Days
* Cohort inquiries: as immediately as possible 
* In the treatment context (e.g. tumor board): immediately

Decisions about requests
************************
If request will be processed is decided by the UAC / Ethics Committee based to their rules. The NSG aims for a future solution where the UAC only needs the approval of the Ethics Committee once for similar requests.

* Available tools: 
	* E-Mail
	* Workflow-Tool (Workflow must be defined, possibly hard coded first, later flexible) 
	* Implementation site specific, one reference implementation

**To be specified:**

* Documentation and administration via HL7 FHIR Task Resource?
* What interfaces are needed for the workflow-decision-tool? 