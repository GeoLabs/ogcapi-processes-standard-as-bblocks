
# Execution unit (Schema)

`ogc.api.processes.part2.schemas.executionUnit` *v1.0.0*

Value of the executionUnit property of an OGC Application Package: one execution unit, or an array of them.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Value of the executionUnit property of an OGC Application Package: one execution unit, or an array of them.

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- `items` is a single schema here, not the one-element array written in the draft: the array form is not a valid schema in OpenAPI 3.0 or JSON Schema 2020-12.

## Schema

```yaml
oneOf:
- $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitBase/schema.yaml
- type: array
  items:
    $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitBase/schema.yaml
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.executionUnit
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnit/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnit/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/executionUnit`

