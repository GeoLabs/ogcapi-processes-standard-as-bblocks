> **DRAFT.** This requirements class mirrors the current editor's draft of OGC API — Processes —
> Part 2: Deploy, Replace, Undeploy (OGC 20-044), available at
> [docs.ogc.org/DRAFTS/20-044.html](https://docs.ogc.org/DRAFTS/20-044.html). It is not yet an
> adopted OGC Standard and should be re-checked against the live draft before being treated as
> final.

## Overview

This requirements class defines the schema of an `OGC Application Package`: a document that
describes a process in sufficient detail so that an implementation of the
[Core](bblocks://ogc.api.processes.part2.requirements.core) requirements class can dynamically
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
[executionUnitBase](bblocks://ogc.api.processes.part2.schemas.executionUnitBase) schema in this
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
