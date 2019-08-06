.. _csp-pseudonymization-anonymization-reference-label:

Pseudo- & Anonymization
~~~~~~~~~~~~~~~~~~~~~~~

* The DSGVO does not apply to anonymous data. Pseudonymised data which can be allocated to natural persons are subject to the DSGVO. See DSGVO recital 26, sentence 2.
* The patient must be informed about the pseudonymisation of the data and consent (see Consents_). 
* Pseudonymisation as a technical measure to minimise the processing of personal data. See DSGVO recital 78, sentence 3.
* In Use Case Infection Control, we only assume that the data is processed internally and do not necessarily have to pseudonymise it, as there is no data exchange between sites.

Aggregated data (depending on the number of cases) are usually anonymous, e.g. mean, number 
There are no truly "anonymous" patient records (danger of re-identification based on laboratory data etc...).

* Consent must be considered in the cohort explorer
* Consent before submitting the proposal to the ethics committee, possibly from an implementation perspective? 
* Does the proposal to the ethics committee require a data protection concept? Hauke: Ethics proposals contain a section on data protection.

Process Cross-Site Pseudonymization
***********************************

The cross-site pseudonymization process describes the solution to two distinct problems within the targeted data sharing procedure withing the HiGHmed consortium. Record-linkage: a method to determine if two subject are the same person, and pseudonym generation: a method to generate a study specific identifier that can be linked back to an individual, but does not identify the subject directly.

Record-linkage
==============

Record-linkage will be implemented using the open source bloomfilter implementation `Mainzelliste`_. To comply with the principals of privacy preserving record linkage [`Schnell et. al 2009`_], only hashed values of directly identifying information (e.g. given name, surname) will be send to the trusted thrird party. In addition a site unique identifier will be send and used for generating a project specific pseudonym.

.. _Mainzelliste: http://www.unimedizin-mainz.de/imbei/informatik/ag-verbundforschung/mainzelliste.html
.. _Schnell et. al 2009: https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/1472-6947-9-41

.. _pseudonym-generation:

Pseudonym-generation
====================

Project specific pseudonyms are generated based on an symetric encryption of site unique identifiers. The following formular illustartes the pseudonym structure:

.. math::

    pseudonym = aes_{\mathrm{256}}(\{site_1: id_1, ..., site_n: id_n\})

AES will be used in chiper block chaining mode (CBC) with a project specific static 128 bit initialization vector and a 256 bit project specific symetric key.

Cross-Site Pseudonymization Use Cases
=====================================

Multiple use cases may require the use of cross-site pseudonymization: cross-site feasibility studies with exact results, cross-site distributed data analysis with anonymous results as well as cross-site data sharing with multiple sites acting as data source and one site acting as a data target. The following BPMN diagram contains the cross-site data sharing process.

Cross-Site data sharing process
-------------------------------

.. raw:: html

   <iframe src="../_static/bpmn-navigated-viewer.html#HiGHmed_DataSharing_Pseudonymization.bpmn" height="300px" width="100%"></iframe> 

Minimal requirements for a data supplying site
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Service for acessing patient master data (given name, surname, date of birth, etc.) based on the patient number used in the OpenEHR repository and other data sources (XDS, XDS-I).
Service for generating N-gram hashes (Mainzellisten-Kontrollnumerngenerator).
Service for asymmetrically encrypting medical data (MDAT) in OpenEHR result sets using the receiving locations public-key, and supplement patient numbers with N-gram hashes of master data.

Minimum requirements for a data receiving site
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Service to decrypt (asymmetrically encrypted) MDAT in OpenEHR result sets unsing the receiving locations private-key.


Procedure at data supplying site
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A data request needs to be approved beforehand.

#. Accept request with AQL (FHIR Task starts process)
#. Execute AQL against OpenEHR
#. Query master data using patient numbers in OpenEHR result set
#. Calculate N-gram hashes with Mainzellisten-Kontrollnumerngenerator locally
#. Write N-gram hashes in OpenEHR result set
#. Encryption MDAT in OpenEHR result asymmetrically, using the public-key of the receiving site
#. Send OpenEHR result set with encrypted MDAT, patient numbers and N-gram hashes to data trustee. To "send" the data is stored in the local FHIR endpoint by the Business Process Engine and a FHIR Task to start the next process step is stored at the data trustee's endpoint

Procedure at data trustee
^^^^^^^^^^^^^^^^^^^^^^^^^

#. Collect OpenEHR result sets from all locations involved (in the project). A per site FHIR Task starts collection process
#. Merge OpenEHR result sets (if more than one site)
#. Extract N-gram hashes and patient numbers from the OpenEHR result sets and create a temporary Mainzelliste with N-gram hashes (frist order pseudonymization aka record linkage)
#. Based on linked and not linked subjects, generate symetrically encrypted pseudonyms using the described algorithm (:ref:`pseudonym-generation`) (second order pseudonymization). A project-specific key is used. This key is known only to the data trustee and must be kept protected until the end of the project, at wich point the key is destroyed.
#. Insert project-specific pseudonyms in OpenEHR result sets
#. Send merged OpenEHR result set to data receiver. To "send" the data is stored in the data trustees FHIR endpoint by the Business Process Engine and a FHIR Task to start the next process step at the data receiving site is stored in the receiving sites endpoint.

Procedure at data receiving site
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Receive OpenEHR result set. A FHIR task starts the "reception". The receiving process downloads the result set from the FHIR endpoint of the data trustee.
#. Decrypt MDAT in OpenEHR result set using the receiving sites private-key
#. Process data
