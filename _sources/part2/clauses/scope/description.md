> **DRAFT.** OGC API — Processes — Part 2: Deploy, Replace, Undeploy (OGC 20-044) is not yet an
> adopted OGC Standard. This content mirrors the current editor's draft and should be re-checked
> against [the live draft](https://docs.ogc.org/DRAFTS/20-044.html) before being treated as final.

The OGC API — Processes — Part 2 Standard is an extension to the [OGC API — Processes — Part 1:
Core](bblocks://ogc.api.processes.part1.requirements.core) Standard and defines the behavior of a
server that supports the ability to dynamically add, replace and/or undeploy processes via an
OGC API — Processes implementation instance.

Specifically, the Part 2 Standard specifies:

- How to deploy a new process.
- How to replace an existing process.
- How to undeploy an existing process.
- How to retrieve the application package last used to deploy or replace a process.

The following table crosswalks each of the resource endpoints discussed in this Standard with the
HTTP methods POST, PUT, DELETE and GET. Each intersecting cell either contains the name of the
operation for that combination of resource endpoint and HTTP method, or "n/a" to indicate that
this Standard does not specify any behavior for that combination.

| Resource endpoint | POST | PUT | DELETE | GET |
|---|---|---|---|---|
| `/processes` | deploy | n/a | n/a | n/a |
| `/processes/{processID}` | n/a | replace | undeploy | n/a |
| `/processes/{processID}/package` | n/a | n/a | n/a | package retrieval |

Deploying or replacing a process requires that a formal description of the new or replacement
process be provided by the client. This Standard does not mandate that a specific process
description language or vocabulary be used, but the draft defines further conformance classes to
promote interoperability — including `OGC Application Package` and `CWL` (Common Workflow
Language) — that are out of scope of this Core requirements class and not yet built in this
register.
