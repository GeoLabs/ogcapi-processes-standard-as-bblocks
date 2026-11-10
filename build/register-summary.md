# OGC API - Processes (Standard as Building Blocks)

OGC API — Processes, authored as Building Blocks. This is a proof-of-concept demonstrating the
"OGC Standards as BBs" methodology, where the standards document is generated from a set of
Building Blocks rather than from AsciiDoc source. Covers Part 1: Core and Part 2: Deploy,
Replace, Undeploy (the latter still a DRAFT standard, not yet adopted).


This repository contains the Building Blocks for OGC API — Processes Part 1: Core (OGC 18-062r3)
and OGC API — Processes Part 2: Deploy, Replace, Undeploy (OGC 20-044, **DRAFT**, not yet
adopted). It demonstrates the [OGC Standards as BBs](https://github.com/opengeospatial/ogcapi-processes/blob/master/docs/ogc-standards-as-bblocks.md)
proposal, where normative requirements, conformance tests, schemas, and prose are all co-located
in a Building Block, and the standards document is generated from the BB set.

New BB types introduced: `requirements-class`, `clause`, `terms`, `references`.
New `bblock.json` fields: `clause-index`, `normative`, `standardization-target`.


## Building Blocks

### `ogc.api.processes.part1.v2.annexes.ats` — Abstract Test Suite

**Type:** clause

Annex A (normative) of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): introduction and layout of the conformance classes and abstract tests.

### `ogc.api.processes.part1.v2.annexes.bibliography` — Bibliography

**Type:** references

Bibliography of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.annexes.revisionHistory` — Revision history

**Type:** clause

Annex B (informative) of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): revision history.

### `ogc.api.processes.part1.v2.clauses.acknowledgements` — Acknowledgements

**Type:** clause

Acknowledgements of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.clauses.additionalBuildingBlocks` — Additional API Building Blocks

**Type:** clause

Additional API building blocks of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): alternative process descriptions and paths.

### `ogc.api.processes.part1.v2.clauses.collections` — Collections

**Type:** clause

Collections clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3), grouping the Collection Input, Remote Collections, Collection Output and Local Filtering requirements classes.

### `ogc.api.processes.part1.v2.clauses.conformance` — Conformance

**Type:** clause

Conformance clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): the sixteen requirements / conformance classes.

### `ogc.api.processes.part1.v2.clauses.conventions` — Conventions

**Type:** clause

Conventions used throughout OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.v2.clauses.encodings` — Requirements classes for encodings

**Type:** clause

Encodings clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3), grouping the JSON and HTML requirements classes.

### `ogc.api.processes.part1.v2.clauses.mediaTypes` — Media Types

**Type:** clause

Media types and profile identifiers of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.clauses.openapi` — OpenAPI requirements classes

**Type:** clause

OpenAPI clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3), grouping the OpenAPI Specification, OpenAPI 3.0 and OpenAPI 3.1 requirements classes.

### `ogc.api.processes.part1.v2.clauses.overview` — Overview

**Type:** clause

Overview clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): Web Processing Service, resources, encodings and execution modes.

### `ogc.api.processes.part1.v2.clauses.preface` — Preface

**Type:** clause

Preface of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.clauses.references` — Normative References

**Type:** references

Normative references for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.v2.clauses.scope` — Scope

**Type:** clause

Scope clause for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.v2.clauses.securityConsiderations` — Security Considerations

**Type:** clause

Security considerations of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): HTTP GET operations, the execute operation and the dismiss operation.

### `ogc.api.processes.part1.v2.clauses.submitters` — Submitters

**Type:** clause

Submitters of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.clauses.submittingOrganizations` — Submitting Organizations

**Type:** clause

Organizations that submitted OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.clauses.terms` — Terms and Definitions

**Type:** terms

Terms, definitions and abbreviated terms for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.v2.requirements.callback` — Callback

**Type:** requirements-class

Requirements class “Callback” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): notification of completed jobs.

### `ogc.api.processes.part1.v2.requirements.collectionInput` — Collection Input

**Type:** requirements-class

Requirements class “Collection Input” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): OGC API collections as process inputs.

### `ogc.api.processes.part1.v2.requirements.collectionOutput` — Collection Output

**Type:** requirements-class

Requirements class “Collection Output” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): process execution triggered through OGC API data access mechanisms.

### `ogc.api.processes.part1.v2.requirements.dismiss` — Dismiss

**Type:** requirements-class

Requirements class “Dismiss” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): cancelling active jobs or deleting completed jobs.

### `ogc.api.processes.part1.v2.requirements.html` — HTML

**Type:** requirements-class

Requirements class “HTML” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): HTML encoding of the API responses.

### `ogc.api.processes.part1.v2.requirements.jobList` — Job list

**Type:** requirements-class

Requirements class “Job list” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): list of jobs with optional filtering.

### `ogc.api.processes.part1.v2.requirements.kvpExecute` — KVP-encoded Execute

**Type:** requirements-class

Requirements class “KVP-encoded Execute” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): process inputs encoded as query parameters of an HTTP GET request.

### `ogc.api.processes.part1.v2.requirements.localFiltering` — Local Filtering

**Type:** requirements-class

Requirements class “Local Filtering” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): filtering of input values by the processing server.

### `ogc.api.processes.part1.v2.requirements.oas` — OpenAPI Specification

**Type:** requirements-class

Requirements class “OpenAPI Specification” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.requirements.oas30` — OpenAPI Specification 3.0

**Type:** requirements-class

Requirements class “OpenAPI Specification 3.0” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.requirements.oas31` — OpenAPI Specification 3.1

**Type:** requirements-class

Requirements class “OpenAPI Specification 3.1” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.requirements.ogcProcessDescription` — OGC Process Description

**Type:** requirements-class

Requirements class “OGC Process Description” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): a JSON information model describing the interface of a process.

### `ogc.api.processes.part1.v2.requirements.queryParamProfile` — Profile query parameter

**Type:** requirements-class

Requirements class “Profile query parameter” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

### `ogc.api.processes.part1.v2.requirements.remoteCollections` — Remote Collections

**Type:** requirements-class

Requirements class “Remote Collections” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): collections of other OGC API deployments as process inputs.

### `ogc.api.processes.part2.v1.annexes.ats` — Abstract Test Suite

**Type:** clause

Annex A (normative) of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT): introduction and layout of the conformance classes and abstract tests.

### `ogc.api.processes.part2.v1.annexes.bibliography` — Bibliography

**Type:** references

Bibliography of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.annexes.revisionHistory` — Revision History

**Type:** clause

Revision history of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.conformance` — Conformance

**Type:** clause

Conformance clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.conventions` — Conventions and background

**Type:** clause

Conventions and background for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.mediaTypes` — Media Types

**Type:** clause

Media types clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.openapi` — OpenAPI 3.0

**Type:** clause

OpenAPI 3.0 clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.references` — Normative References

**Type:** references

Normative references for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.scope` — Scope

**Type:** clause

Scope clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.securityConsiderations` — Security Considerations

**Type:** clause

Security considerations for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.clauses.submitters` — Submitters

**Type:** clause

Submitters of OGC API — Processes Part 2 (DRAFT).

### `ogc.api.processes.part2.v1.clauses.submittingOrganizations` — Submitting Organizations

**Type:** clause

Organizations that submitted OGC API — Processes Part 2 (DRAFT).

### `ogc.api.processes.part2.v1.clauses.terms` — Terms and Definitions

**Type:** terms

Terms, definitions and abbreviated terms for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.v1.requirements.dru` — Deploy, Replace, Undeploy

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 2 (DRAFT). Specifies the fundamental operations a server must support to dynamically deploy, replace, undeploy processes, and retrieve the last application package used to deploy or replace a process: POST /processes, PUT /processes/{processID}, DELETE /processes/{processID}, and GET /processes/{processID}/package.

### `ogc.api.processes.part2.v1.requirements.ogcapppkg` — OGC Application Package

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Defines the schema of an OGC Application Package document — a formal process description used to dynamically deploy or replace a process — and the media type (application/ogcapppkg+json) used to carry it in requests and responses.

### `ogc.api.processes.part2.v1.requirements.cwl` — CWL

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Enables support for the Common Workflow Language (CWL) as a process description encoding, either embedded in an OGC Application Package or sent directly as the deploy/replace request body.

### `ogc.api.processes.part2.v1.requirements.docker` — Docker

**Type:** requirements-class

Conformance class for OGC API - Processes Part 2 (DRAFT). Defines requirements for Docker-based execution units in OGC Application Packages.

### `ogc.api.processes.part1.v2.requirements.core` — Core

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 1. Specifies the fundamental operations a server must support: landing page, conformance declaration, process list, process description, process execution, job status, and job results.

### `ogc.api.processes.part1.v2.requirements.json` — JSON

**Type:** requirements-class

Requirements class for JSON encoding. Requires that all supported API endpoints respond with application/json when requested.

