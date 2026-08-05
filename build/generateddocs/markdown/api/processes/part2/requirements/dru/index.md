
# Deploy, Replace, Undeploy (Requirements-class)

`ogc.api.processes.part2.requirements.dru` *v1.0.0*

Core requirements class for OGC API — Processes Part 2 (DRAFT). Specifies the fundamental operations a server must support to dynamically deploy, replace, undeploy processes, and retrieve the last application package used to deploy or replace a process: POST /processes, PUT /processes/{processID}, DELETE /processes/{processID}, and GET /processes/{processID}/package.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

> **DRAFT.** This requirements class mirrors the current editor's draft of OGC API — Processes —
> Part 2: Deploy, Replace, Undeploy (OGC 20-044), available at
> [docs.ogc.org/DRAFTS/20-044.html](https://docs.ogc.org/DRAFTS/20-044.html). It is not yet an
> adopted OGC Standard and should be re-checked against the live draft before being treated as
> final.

## Overview

A server that implements the `Deploy, Replace, Undeploy` requirements class provides the ability
to dynamically deploy, replace and undeploy processes on top of an [OGC API — Processes — Part 1:
Core](bblocks://ogc.api.processes.part1.requirements.core) implementation.

- The HTTP POST method is used to deploy a new process to the API.
- The HTTP PUT method is used to replace the definition of a previously deployed process.
- The HTTP DELETE method is used to undeploy a previously deployed process.
- The HTTP GET method, at a dedicated `/package` sub-resource, is used to retrieve the last
  application package used to deploy or replace a process.

Deploying or replacing a process requires that a formal description of the new or replacement
process be provided by the client. This requirements class does not mandate a specific process
description language or vocabulary; the draft standard defines further conformance classes (`OGC
Application Package`, `Docker`, `CWL`) to promote interoperability around specific encodings —
none of those are in scope of this Core requirements class.

The draft also recognizes that a server may be deployed with a set of static, built-in processes
that are immutable and cannot be removed or modified through this requirements class's
operations. The optional `mutable` property on a process summary indicates whether a given
process can be replaced or undeployed.

## API Resources

| Resource | Path | HTTP method |
|---|---|---|
| Deploy a process | `/processes` | POST |
| Replace a process | `/processes/{processID}` | PUT |
| Undeploy a process | `/processes/{processID}` | DELETE |
| Application package retrieval | `/processes/{processID}/package` | GET |

<!-- requirements -->

The following section covers all 22 requirements of the `Deploy, Replace, Undeploy` requirements
class as currently drafted. Test coverage in this checkpoint is intentionally partial (a couple of
representative fixtures), mirroring the same "PoC scope" approach used for Part 1's own Core
requirements class in this register.

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/requirements/dru`

