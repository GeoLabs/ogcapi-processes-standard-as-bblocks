
# Process summary (Deploy response) (Schema)

`ogc.api.processes.part2.schemas.processSummary` *v1.0.0*

Summary description of a deployed process, returned in the body of a Deploy response (Requirement /req/deploy-replace-undeploy/deploy-response-body).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Summary description of a deployed process, returned in the body of a Deploy response (Requirement /req/deploy-replace-undeploy/deploy-response-body).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

## Schema

```yaml
allOf:
- $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/descriptionType/schema.yaml
- type: object
  required:
  - id
  - version
  properties:
    id:
      type: string
    version:
      type: string
    jobControlOptions:
      type: array
      items:
        $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/jobControlOptions/schema.yaml
    links:
      type: array
      items:
        $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/link/schema.yaml
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.processSummary
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/processSummary/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/processSummary/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/processSummary`

