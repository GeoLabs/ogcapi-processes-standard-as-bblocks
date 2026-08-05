
# OGC Application Package (Requirements-class)

`ogc.api.processes.part2.requirements.ogcapppkg` *v1.0.0*

Conformance class for OGC API — Processes Part 2 (DRAFT). Defines the schema of an OGC Application Package document — a formal process description used to dynamically deploy or replace a process — and the media type (application/ogcapppkg+json) used to carry it in requests and responses.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

> **DRAFT.** This requirements class mirrors the current editor's draft of OGC API — Processes —
> Part 2: Deploy, Replace, Undeploy (OGC 20-044), available at
> [docs.ogc.org/DRAFTS/20-044.html](https://docs.ogc.org/DRAFTS/20-044.html). It is not yet an
> adopted OGC Standard and should be re-checked against the live draft before being treated as
> final.

## Overview

This requirements class defines the schema of an `OGC Application Package`: a document that
describes a process in sufficient detail so that an implementation of the
[Core](bblocks://ogc.api.processes.part2.requirements.dru) requirements class can dynamically
deploy that process and make it accessible via [OGC API — Processes — Part 1:
Core](bblocks://ogc.api.processes.part1.requirements.core).

An OGC Application Package includes:

- A formal description of the process — what inputs it takes, what outputs it generates (optional;
  if absent, the process interface must be inferred from the execution unit).
- Either an inline or by-reference execution unit describing the code the server needs to execute
  whenever the process is invoked.
- Additional resource information the server may require to establish an execution environment for
  the execution unit.

Two families of execution unit are anticipated by the draft: units where the executable code is
encapsulated in a container (e.g. Docker), and units encoded as a workflow executed by some
workflow runner (e.g. [CWL](bblocks://ogc.api.processes.part2.requirements.cwl)). The Docker/OCI
container form is illustrated below for context, but its full schema belongs to a separate
"Docker" conformance class not yet built in this register — the
[executionUnitBase](bblocks://ogc.api.processes.v2.schemas.executionUnitBase) schema in this
register therefore only constrains that branch loosely (a generic object) pending that future
work.

```json
{
  "executionUnit": {
    "type": "docker",
    "value": {
      "image": "mydocker/ndvi:latest",
      "bindings": {
        "inputBindings": {
          "inputImage": {
            "prefix": "inputsImages=",
            "inputSeparator": ","
          }
        },
        "outputBindings": {
          "outputImage": {
            "glob": "$(\"/outputs/ndvi_\" + inputs.inputImage.basename)"
          }
        }
      },
      "deployment": "local",
      "config": {
        "cpuMin": 2,
        "cpuMax": 5,
        "memoryMin": 1,
        "memoryMax": 3
      }
    }
  }
}
```

<!-- requirements -->

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/requirements/ogcapppkg`

