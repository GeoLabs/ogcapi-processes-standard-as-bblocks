> **DRAFT.** This requirements class mirrors the current editor's draft of OGC API — Processes —
> Part 2: Deploy, Replace, Undeploy (OGC 20-044), available at
> [docs.ogc.org/DRAFTS/20-044.html](https://docs.ogc.org/DRAFTS/20-044.html). It is not yet an
> adopted OGC Standard and should be re-checked against the live draft before being treated as
> final.

## Overview

This requirements class enables support for the Common Workflow Language (CWL) as a process
description encoding, in two ways:

1. **Embedded in an [OGC Application Package](bblocks://ogc.api.processes.part2.requirements.ogcapppkg).**
   The CWL document is carried as the `executionUnit` property, either by reference (a link to the
   CWL file) or by value (a qualified value carrying the CWL document inline, as a JSON object or
   as an embedded JSON/YAML string). When embedded this way, the `processDescription` property of
   the Application Package does not need to be specified — the process interface can be inferred
   from the CWL value.
2. **Sent directly**, without being embedded in an Application Package: the request body of a
   [deploy or replace](bblocks://ogc.api.processes.part2.requirements.dru) operation is itself a
   CWL document.

### By reference

```json
{
  "executionUnit": {
    "href": "https://raw.githubusercontent.com/EOEPCA/app-snuggs/main/app-package.cwl",
    "type": "application/cwl"
  }
}
```

### By value, as a JSON object

```json
{
  "executionUnit": {
    "mediaType": "application/cwl",
    "value": { "cwlVersion": "v1.2", "class": "CommandLineTool" }
  }
}
```

### By value, as an embedded string

```json
{
  "executionUnit": {
    "mediaType": "application/cwl+yaml",
    "value": "cwlVersion: 'v1.2'\nclass: CommandLineTool\n..."
  }
}
```

### The `w` query parameter

When a CWL document contains more than one workflow, the `w` query parameter selects which
workflow identifier to deploy. If omitted, the first workflow found is deployed. If the value of
`w` cannot be located in the request body, the server responds with an HTTP `400` and an
[exception](bblocks://ogc.api.processes.v1.schemas.exception) of type
`https://www.opengis.net/def/exceptions/ogcapi-processes-2/1.0/workflow-not-found`.

<!-- requirements -->
