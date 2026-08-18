
# Docker (Requirements-class)

`ogc.api.processes.part2.requirements.docker` *v1.0.0*

Conformance class for OGC API - Processes Part 2 (DRAFT). Defines requirements for Docker-based execution units in OGC Application Packages.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

> **DRAFT.** This requirements class mirrors the current editor's draft of OGC API - Processes -
> Part 2: Deploy, Replace, Undeploy (OGC 20-044), available at
> [docs.ogc.org/DRAFTS/20-044.html](https://docs.ogc.org/DRAFTS/20-044.html). It is not yet an
> adopted OGC Standard and should be re-checked against the live draft before being treated as
> final.

## Overview

This requirements class defines how a server can describe Docker-based execution units in an
OGC Application Package. It covers:

- the Docker execution unit schema;
- the required execution unit `type` and `image` properties;
- deployment-location semantics;
- execution configuration parameters;
- input/output bindings and expression usage.

This class depends on:

- [Deploy, Replace, Undeploy](bblocks://ogc.api.processes.part2.requirements.dru), and
- [OGC Application Package](bblocks://ogc.api.processes.part2.requirements.ogcapppkg).

<!-- requirements -->

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/requirements/docker`

