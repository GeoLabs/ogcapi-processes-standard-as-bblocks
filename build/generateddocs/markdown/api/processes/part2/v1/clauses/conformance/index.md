
# Conformance (Clause)

`ogc.api.processes.part2.v1.clauses.conformance` *v1.0.0*

Conformance clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The OGC API — Processes — Part 2 Standard defines the following requirements classes.

The main requirements class is:

- [Deploy, Replace, Undeploy](bblocks://ogc.api.processes.part2.v1.requirements.dru).

This class specifies requirements that any Web API implementing Processes Part 2 must conform with.

The `Deploy, Replace, Undeploy` class does not mandate a specific encoding or format for the formal definition of a process. However, the Part 2 extension defines the following conformance class:

- [OGC Application Package](bblocks://ogc.api.processes.part2.v1.requirements.ogcapppkg)

The `OGC Application Package` class defines the schema of a document that formally defines the inputs, outputs and other necessary metadata about a process that is to be dynamically deployed through the API.

The Application Package encoding is not mandatory. An implementation of this Standard may choose to implement some other process description instead. That said, the `Deploy, Replace, Undeploy` conformance class includes recommendations to support the `OGC Application Package`.

A requirement class is dedicated to the deployment of containers as processes:

- [Docker](bblocks://ogc.api.processes.part2.v1.requirements.docker)

In addition to the previous encoding, another conformance class is provided to enable support for the Common Workflow Language (CWL):

- [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl)

The standardization target for all Conformance class defined in this Standard is “Web API”.

Conformance with this Standard shall be checked using all the relevant tests specified in [\[ats\]](#sec-A) of this document. The framework, concepts, and methodology for testing, and the criteria to be achieved to claim conformance are specified in the OGC Compliance Testing Policies and Procedures and the OGC Compliance Testing web site.

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/v1/clauses/conformance`

