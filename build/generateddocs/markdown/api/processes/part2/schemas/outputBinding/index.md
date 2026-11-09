
# Docker output binding (Schema)

`ogc.api.processes.part2.schemas.outputBinding` *v1.0.0*

How a process output is retrieved from a Docker execution unit (Requirement /req/docker/output-binding).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

How a process output is retrieved from a Docker execution unit (Requirement /req/docker/output-binding).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

## Schema

```yaml
type: object
description: Defines how to retrieve the output result from the command.
properties:
  glob:
    description: ". Wildcard pattern to find the output on disk or mounted volume.\n.
      Uses UNIX \"glob\" wildcard patterns (see: \"man 7 glob\").\n. See inputBinding.yaml
      for referencing input values in an output\n  binding \"glob\" expression."
    oneOf:
    - type: string
    - type: array
      items:
        type: string
additionalProperties: true
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.outputBinding
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/outputBinding/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/outputBinding/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/outputBinding`

