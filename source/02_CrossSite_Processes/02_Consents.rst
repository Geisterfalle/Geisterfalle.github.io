.. _csp-consents-reference-label:

Consents
~~~~~~~~

Questions
************
* Which processes can be agreed to?
* At which level of abstraction can consent be given?
* How are consents mapped technically?

NSG approval
*************
* Data transfer for research purposes
* Bio-material storage
* Retrieval of data from health insurance companies (possibly in contradiction to §75 SGB X)
* Consent to establishment of contact

Information on the planned procedure for use case consents
***********************************************************
* Infection Control: Legal foundation --> Treatment contract and infection protection law.
* Cardiology: Consent for 
	* Recontacting
	* Retrieval of data / documents of other physicians
	* Sensor only when device is provided, possibly in combination with Patient Reported Outcome
	* Patient Reported Outcome, possibly in combination with sensor data
* Oncology: Consent for 
	* Virtual molecular HiGHmed tumor board (incl. patient-related data) - unnecessary if HiGHmed tumor board is used for patient treatment.
	* Search for similar patients
	* Use / acceptance of bio-material

Technical implementation
************************
* All compositions are registered --> APPC possible
* Define Archetype as Resource to Access Archetype Level
* Document can be restricted via metadata
* First submit AQL query, filter result set via APPC

**To be specified:**

* How many are there? 
* How many have really consented? 
* Consent Management / possibly in the patient portal
* Set consent for UAC