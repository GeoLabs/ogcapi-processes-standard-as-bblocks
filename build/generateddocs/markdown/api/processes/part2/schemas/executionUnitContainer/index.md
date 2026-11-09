
# Docker execution unit value (Schema)

`ogc.api.processes.part2.schemas.executionUnitContainer` *v1.0.0*

Value of the value field of a Docker execution unit (Requirement /req/docker/schema).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Value of the value field of a Docker execution unit (Requirement /req/docker/schema).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- `required` is a list here. The draft writes `required: image`, which is not a valid schema.

## Schema

```yaml
type: object
required:
- image
properties:
  image:
    description: Container image reference for the execution unit.
    type: string
  deployment:
    description: Deployment information for the execution unit.
    type: string
    anyOf:
    - type: string
    - enum:
      - local
      - remote
      - hpc
      - cloud
  config:
    type: object
    description: 'Hardware requirements and configuration properties for executing
      the

      process.'
    properties:
      cpuMin:
        description: Minimum number of CPUs required to run the process (unit is CPU
          core).
        type: number
        minimum: 1
      cpuMax:
        description: Maximum number of CPU dedicated to the process (unit is CPU core)
        type: number
      memoryMin:
        description: Minimum RAM memory required to run the application (unit is GB)
        type: number
      memoryMax:
        description: Maximum RAM memory dedicated to the application (unit is GB)
        type: number
      storageTempMin:
        description: Minimum required temporary storage size (unit is GB)
        type: number
      storageOutputsMin:
        description: Minimum required output storage size (unit is GB)
        type: number
      jobTimeout:
        description: Timeout delay for a job execution (in seconds)
        type: number
    additionalProperties: true
  bindings:
    type: object
    properties:
      inputBindings:
        additionalProperties:
          $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/inputBinding/schema.yaml
      outputBindings:
        additionalProperties:
          $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/outputBinding/schema.yaml
additionalProperties: true
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.executionUnitContainer
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitContainer/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitContainer/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/executionUnitContainer`

