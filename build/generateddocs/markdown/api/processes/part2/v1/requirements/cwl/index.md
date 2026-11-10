
# CWL (Requirements-class)

`ogc.api.processes.part2.v1.requirements.cwl` *v1.0.0*

Conformance class for OGC API — Processes Part 2 (DRAFT). Enables support for the Common Workflow Language (CWL) as a process description encoding, either embedded in an OGC Application Package or sent directly as the deploy/replace request body.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Sending CWL embedded in an OGC Application Package

## Overview

<!-- requirements-class -->

This clause defines the requirements for sending a CWL document to the process deployment endpoint (i.e. /processes) embedded in an [OGC Application Package](#sec-7)

Embedding the CWL document in the [OGC Application Package](#sec-7) means that the `processDescription` property does not need to be specified because the description of the process can be inferred from the CWL value specified in the `executionUnit`.

## Specifying the CWL by reference

<!-- requirement: cwl/execution-unit-by-ref -->

Below is an example of a [Deploy request](#sec-6.6) body using a CWL-encoded execution unit by reference.

```json
{
  "executionUnit": {
    "href": "https://raw.githubusercontent.com/EOEPCA/app-snuggs/main/app-package.cwl",
    "type": "application/cwl"
  }
}
```

## Specifying the CWL by value

<!-- requirement: cwl/execution-unit-by-val -->

Below is an example of a [Deploy request](#sec-6.6) body using a qualified value to pass the CWL value. In this example, the CWL is encoded as a JSON object and so the value of the `mediaType` field does not need to explicitly state that the CWL is JSON-encoded. This is implied by the structure of the content of the `value` field.

```json
{
  "executionUnit": {
    "mediaType": "application/cwl",
    "value": { "cwlVersion": "v1.2", "class": "CommandLineTool", ... }
  }
}
```

**Listing 13**

<div class="note">

**NOTE:** The CWL content is truncated for readability.

</div>

Below are other examples of [Deploy request](#sec-6.6) bodies where the CWL value is included as an embedded string within the qualified value. In these cases the value of the `mediaType` field needs to be explicit in order to disambiguate the structure of the string content.

```json
{
  "executionUnit": {
    "mediaType": "application/cwl+json",
    "value": "{ \"cwlVersion\": \"v1.2\", \"class\": \"CommandLineTool\", ... }"
  }
}
```

**Listing 14**

```json
{
  "executionUnit": {
    "mediaType": "application/cwl+yaml",
    "value": "cwlVersion: 'v1.2'\nclass: CommandLineTool\n..."
  }
}
```

**Listing 15**

# Sending CWL directly

## Overview

This clause defines the requirements for sending a CWL document directly to the process deployment endpoint (i.e. `/processes`) without embedding the CWL into an [OGC Application Package](#sec-7)

## CWL request body

<!-- requirement: cwl/body -->

## Multipart CWL request body

<!-- permission: cwl/multipart-cwl-body -->

The following multipart example illustrates one request payload with a root workflow selected by the `start` parameter, with supporting documents referenced by `filename`, `cid:` URI and remote URL combinations. The full contents of the individual [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) documents are not included for simplification. Note that the [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) YAML representation are employed to provide a concise example, but other [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) media-types are permitted in any desired combination.

In the example, the `Content-ID` headers and embedded `id` fields of respective parts are provided to illustrate the expected interpretation of equivalent definitions, but some might be omitted as described in the recommendation text.

The last [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) part illustrates how its corresponding definition can be omitted because of the provided `Content-Location` header. However, each part (including the ones providing the content directly), could also include the `Content-Location` header for complementary identification of their origin if desired.

The last process description part illustrates how additional metadata can be included in the multipart body to refine the definition of the process being deployed, irrespective of its [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) encoding.

```text
Client                                                            Server
  |                                                                 |
  |  POST /processes HTTP/1.1                                       |
  |  Host: example.org                                              |
  |  Content-Type: multipart/related; type="application/cwl+yaml"; start="<workflow-main@example.org>"; boundary="===CWL-BUNDLE==="
  |  Content-ID: <workflow-main@example.com>                        |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/cwl+yaml                             |
  |  Content-ID: <workflow-main@example.org>                        |
  |  Content-Disposition: attachment; filename="workflows/main.cwl" |
  |                                                                 |
  |  cwlVersion: v1.2                                               |
  |  class: Workflow                                                |
  |  id: workflow-main                                              |
  |  steps:                                                         |
  |    by_filename:                                                 |
  |      run: "tools/tool-1.cwl"                                    |
  |      ...  # rest of the definition                              |
  |    by_cid_host:                                                 |
  |      run: "cid:tool-2@example.org"                              |
  |      ...  # rest of the definition                              |
  |    by_cid_uuid:                                                 |
  |      run: "cid:urn:uuid:550e8400-e29b-41d4-a716-446655440002"   |
  |      ...  # rest of the definition                              |
  |    by_remote_url:                                               |
  |      run: "https://example.org/cwl/tools/tool-4.cwl"            |
  |      ...  # rest of the definition                              |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/cwl+yaml                             |
  |  Content-Disposition: attachment; filename="tools/tool-1.cwl"   |
  |  Content-ID: <tool-1@example.org>                               |
  |                                                                 |
  |  cwlVersion: v1.2                                               |
  |  class: CommandLineTool                                         |
  |  id: tool-1                                                     |
  |  ...  # rest of the definition                                  |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/cwl+yaml                             |
  |  Content-ID: <tool-2@example.org>                               |
  |  Content-Disposition: attachment; filename="tools/tool-2.cwl"   |
  |                                                                 |
  |  cwlVersion: v1.2                                               |
  |  class: CommandLineTool                                         |
  |  id: tool-2                                                     |
  |  ...  # rest of the definition                                  |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/cwl+yaml                             |
  |  Content-ID: <urn:uuid:550e8400-e29b-41d4-a716-446655440002>    |
  |  Content-Disposition: attachment; filename="tools/tool-3.cwl"   |
  |                                                                 |
  |  cwlVersion: v1.2                                               |
  |  class: CommandLineTool                                         |
  |  id: tool-3                                                     |
  |  ...  # rest of the definition                                  |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/cwl+yaml                             |
  |  Content-Location: https://example.org/cwl/tools/tool-4.cwl     |
  |  Content-Disposition: attachment; filename="tools/tool-4.cwl"   |
  |                                                                 |
  |  --===CWL-BUNDLE===                                             |
  |  Content-Type: application/json                                 |
  |  Content-Profile: <https://www.opengis.net/def/profile/OGC/0/ogc-process-description>
  |                                                                 |
  |  ...  # additional metadata for the process being deployed      |
  |  --===CWL-BUNDLE===--                                           |
  |---------------------------------------------------------------->|
  |                                                                 |
  |  HTTP/1.1 201 Created                                           |
  |  Location: /processes/{processID}                               |
  |<----------------------------------------------------------------|
```

**Listing 16**

The following partial example illustrates how the main CWL part can be represented by the `#main` identifier in accordance to the [CWL Packed documents](https://www.commonwl.org/v1.2/CommandLineTool.html#Packed_documents) representation, instead of using the multipart `start` parameter. In this case, the `Content-ID` header of the entire request (i.e.: [`<workflow-main@example.com>`](mailto:workflow-main@example.com)) indicates that the `{processID}` should be `workflow-main`, while the `Content-ID` within the part (i.e.: [`<#main@example.com>`](mailto:main@example.com)) indicates that this part is the main [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) document. The rest of the definition is identical to the previous example.

```text
Client                                                            Server
  |                                                                 |
  | POST /processes HTTP/1.1                                        |
  | Host: example.org                                               |
  | Content-Type: multipart/related; type="application/cwl+yaml"; boundary="===CWL-BUNDLE==="
  | Content-ID: <workflow-main@example.com>                         |
  |                                                                 |
  | --===CWL-BUNDLE===                                              |
  | Content-Type: application/cwl+yaml                              |
  | Content-ID: <#main@example.org>                                 |
  | Content-Disposition: attachment; filename="workflows/main.cwl"  |
  |                                                                 |
  | cwlVersion: v1.2                                                |
  | class: Workflow                                                 |
  | id: workflow-main                                               |
  | ...  # rest of the definition                                   |
  |                                                                 |
  | --===CWL-BUNDLE===                                              |
  | ...  # other parts are identical to the previous example        |
  | --===CWL-BUNDLE===--                                            |
  .                                                                 .
  .                                                                 .
  .                                                                 .
```

**Listing 17**

# w parameter

When encoded in CWL processes are identified as instances of the workflow class.

<!-- requirement: cwl/deploy-w-param -->

<!-- requirement: cwl/deploy-exception-workflow-not-found -->

# Media types in operations

<!-- requirement: cwl/media-type-request -->

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)
* [Common Workflow Language v1.2](https://www.commonwl.org/v1.2/)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/v1/requirements/cwl`

