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

### `ogc.api.processes.part2.clauses.references` — Normative References

**Type:** references

Normative references for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.scope` — Scope

**Type:** clause

Scope clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.clauses.terms` — Terms and Definitions

**Type:** terms

Terms, definitions and abbreviated terms for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

### `ogc.api.processes.part2.schemas.format` — Format schema

**Type:** schema

Media type, encoding and schema of a value (DRAFT). Base fragment of the qualifiedValue schema used by the executionUnit schema.

### `ogc.api.processes.part2.schemas.collectionValue` — Collection value schema

**Type:** schema

A value sourced from an OGC API collection (DRAFT), reached via the qualifiedValue/value/valueNoObject schema chain used by the executionUnit schema. Tangential to Application Package/CWL proper — reproduced for schema-chain fidelity.

### `ogc.api.processes.part2.schemas.valueNoObject` — Value (no object) schema

**Type:** schema

Non-object value variants (DRAFT): scalar, array, binary value, bounding box, or OGC API collection-sourced value. Reuses Part 1's imported binaryInputValue and bbox schemas where the shape matches.

### `ogc.api.processes.part2.schemas.staticIndicator` — Static indicator schema

**Type:** schema

Extends the Part 1 processSummary schema with the optional 'mutable' property (DRAFT), indicating whether a process is a static/built-in immutable process or a dynamically deployed mutable one.

### `ogc.api.processes.part2.schemas.value` — Value schema

**Type:** schema

The 'value' property of a qualified value (DRAFT): any non-object value, or a JSON object (e.g. an inline CWL document).

### `ogc.api.processes.part2.schemas.qualifiedValue` — Qualified value schema

**Type:** schema

A value qualified by a media type / encoding / schema (DRAFT), used to describe execution units inline within an OGC Application Package. Not part of the imported Part 1 payload register; authored locally since Part 2 needs it for the executionUnit schema.

### `ogc.api.processes.part2.schemas.executionUnitBase` — Execution unit base schema

**Type:** schema

Base schema of a single execution unit (DRAFT): either a link to the execution unit, or an inline qualified value describing a container image, a CWL script, or another custom encoding.

### `ogc.api.processes.part2.schemas.executionUnit` — Execution unit schema

**Type:** schema

Schema of the 'executionUnit' property of an OGC Application Package (DRAFT): either a single execution unit or an array of execution units.

### `ogc.api.processes.part2.schemas.ogcapppkg` — OGC Application Package schema

**Type:** schema

Schema of an OGC Application Package document (DRAFT): a formal description of a process to be dynamically deployed, made of an optional process description and a required execution unit.

### `ogc.api.processes.part1.requirements.core` — Core

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 1. Specifies the fundamental operations a server must support: landing page, conformance declaration, process list, process description, process execution, job status, and job results.

### `ogc.api.processes.part1.requirements.json` — JSON

**Type:** requirements-class

Requirements class for JSON encoding. Requires that all supported API endpoints respond with application/json when requested.

### `ogc.api.processes.part2.requirements.core` — Deploy, Replace, Undeploy

**Type:** requirements-class

Core requirements class for OGC API — Processes Part 2 (DRAFT). Specifies the fundamental operations a server must support to dynamically deploy, replace, undeploy processes, and retrieve the last application package used to deploy or replace a process: POST /processes, PUT /processes/{processID}, DELETE /processes/{processID}, and GET /processes/{processID}/package.

### `ogc.api.processes.part2.requirements.ogcapppkg` — OGC Application Package

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Defines the schema of an OGC Application Package document — a formal process description used to dynamically deploy or replace a process — and the media type (application/ogcapppkg+json) used to carry it in requests and responses.

### `ogc.api.processes.part2.requirements.cwl` — CWL

**Type:** requirements-class

Conformance class for OGC API — Processes Part 2 (DRAFT). Enables support for the Common Workflow Language (CWL) as a process description encoding, either embedded in an OGC Application Package or sent directly as the deploy/replace request body.

