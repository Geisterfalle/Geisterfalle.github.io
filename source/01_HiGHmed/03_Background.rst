.. _h-background-reference-label:

Background and Basic Concepts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The HiGHmed Platform aims to better interconnect the research domain and the care provision domain 
by establishing a harmonized data exchange layer between independent organizations and by providing means 
to build semantic interoperable software applications based on a standardized application programming interface (API). 
We understand the HiGHmed Platform as a socio-technical process rather than a software solution: in order to get the platform to work properly, 
the establishment of a shared information governance and management between the HiGHmed partners is needed. On the one hand, this requires the incorporation of 
governance rules and standard operating procedures. On the other hand, technical components as an information model governance tool and a shared terminology service will need to be established. 
The model governance tool will serve as a library for reusable and formal definitions of clinical information models. In other words, HiGHmed establishdx 
a cross-enterprise data dictionary to collaboratively harmonize the structured documentation within the particular hospital information systems. Concurrently, 
by establishing the HiGHmed Platform, participating organizations create capacities to integrate data into a single data repository which can then be used 
for the support of care provision and research alike. Moreover, the HiGHmed Platform can be used to create new applications based on a shared semantic layer. 
This way, future data integration tasks can be highly facilitated. 
This document provides an overview of the HiGHmed Platform architecture. 
Our approach to provide a specification and platform implementation is deliberatively inspired by the processes 
established by organizations like IHE and Apache Foundation. While we start with a basic configuration, new versions of the platform specification 
will be created, implemented, tested and released. This overview document links to different specifications which themselves may also link to other specifications. 
Where applicable, the most relevant parts of the standards/specifications referenced are explained in sufficient detail. We hope that by doing so, we find a 
good balance between formal correctness and comprehensibility.

.. literalinclude:: sources/HelloWorld.java
   :language: java
   :linenos: