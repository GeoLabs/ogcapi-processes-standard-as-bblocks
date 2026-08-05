
# Format schema (Schema)

`ogc.api.processes.part2.schemas.format` *v1.0.0*

Media type, encoding and schema of a value (DRAFT). Base fragment of the qualifiedValue schema used by the executionUnit schema.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
type: object
properties:
  mediaType:
    type: string
  encoding:
    type: string
  schema:
    oneOf:
    - type: string
      format: url
    - type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/format/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/format/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/format`

