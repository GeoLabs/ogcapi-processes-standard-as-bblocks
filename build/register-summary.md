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

### `ogc.api.processes.part1.clauses.conventions` — Conventions

**Type:** clause

Conventions used throughout OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.clauses.references` — Normative References

**Type:** references

Normative references for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.clauses.scope` — Scope

**Type:** clause

Scope clause for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part1.clauses.terms` — Terms and Definitions

**Type:** terms

Terms, definitions and abbreviated terms for OGC API — Processes Part 1: Core.

### `ogc.api.processes.part2.annexes.ats` — Abstract Test Suite

**Type:** clause

Annex A (normative) of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT): introduction and layout of the conformance classes and abstract tests.

### `ogc.api.processes.part2.annexes.bibliography` — Bibliography

**Type:** references

Bibliography of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.annexes.revisionHistory` — Revision History

**Type:** clause

Revision history of OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.conformance` — Conformance

**Type:** clause

Conformance clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.conventions` — Conventions and background

**Type:** clause

Conventions and background for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.mediaTypes` — Media Types

**Type:** clause

Media types clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.openapi` — OpenAPI 3.0

**Type:** clause

OpenAPI 3.0 clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.references` — Normative References

**Type:** references

Normative references for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.scope` — Scope

**Type:** clause

Scope clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.securityConsiderations` — Security Considerations

**Type:** clause

Security considerations for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.submitters` — Submitters

**Type:** clause

Submitters of OGC API — Processes Part 2 (DRAFT).

### `ogc.api.processes.part2.clauses.submittingOrganizations` — Submitting Organizations

**Type:** clause

Organizations that submitted OGC API — Processes Part 2 (DRAFT).

### `ogc.api.processes.part2.clauses.terms` — Terms and Definitions

**Type:** terms

Terms, definitions and abbreviated terms for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.schemas.inputBinding` — Docker input binding

**Type:** schema

How a process input is passed to a Docker execution unit (Requirement /req/docker/input-binding).

### `ogc.api.processes.part2.schemas.outputBinding` — Docker output binding

**Type:** schema

How a process output is retrieved from a Docker execution unit (Requirement /req/docker/output-binding).

### `ogc.api.processes.part2.schemas.executionUnitContainer` — Docker execution unit value

**Type:** schema

Value of the value field of a Docker execution unit (Requirement /req/docker/schema).

### `ogc.api.processes.part2.schemas.processSummary` — Process summary (Deploy response)

**Type:** schema

Summary description of a deployed process, returned in the body of a Deploy response (Requirement /req/deploy-replace-undeploy/deploy-response-body).

### `ogc.api.processes.part2.schemas.executionUnitBase` — Execution unit (single)

**Type:** schema

One execution unit: a link, or a qualified value holding a container image, a CWL document or a custom type.

### `ogc.api.processes.part2.schemas.executionUnit` — Execution unit

**Type:** schema

Value of the executionUnit property of an OGC Application Package: one execution unit, or an array of them.

### `ogc.api.processes.part2.schemas.ogcapppkg` — OGC Application Package

**Type:** schema

Schema of an OGC Application Package document (Requirement /req/ogcapppkg/schema).

### `ogc.api.processes.part1.requirements.core` — Core

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 1. Specifies the fundamental operations a server must support: landing page, conformance declaration, process list, process description, process execution, job status, and job results.

### `ogc.api.processes.part1.requirements.json` — JSON

**Type:** requirements-class

Requirements class for JSON encoding. Requires that all supported API endpoints respond with application/json when requested.

### `ogc.api.processes.part2.requirements.dru` — Deploy, Replace, Undeploy

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 2 (DRAFT). Specifies the fundamental operations a server must support to dynamically deploy, replace, undeploy processes, and retrieve the last application package used to deploy or replace a process: POST /processes, PUT /processes/{processID}, DELETE /processes/{processID}, and GET /processes/{processID}/package.

### `ogc.api.processes.part2.requirements.ogcapppkg` — OGC Application Package

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Defines the schema of an OGC Application Package document — a formal process description used to dynamically deploy or replace a process — and the media type (application/ogcapppkg+json) used to carry it in requests and responses.

### `ogc.api.processes.part2.requirements.cwl` — CWL

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Enables support for the Common Workflow Language (CWL) as a process description encoding, either embedded in an OGC Application Package or sent directly as the deploy/replace request body.

### `ogc.api.processes.part2.requirements.docker` — Docker

**Type:** requirements-class

Conformance class for OGC API - Processes Part 2 (DRAFT). Defines requirements for Docker-based execution units in OGC Application Packages.

