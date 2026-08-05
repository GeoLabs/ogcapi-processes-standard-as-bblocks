
# Execution unit base schema (Schema)

`ogc.api.processes.part2.schemas.executionUnitBase` *v1.0.0*

Base schema of a single execution unit (DRAFT): either a link to the execution unit, or an inline qualified value describing a container image, a CWL script, or another custom encoding.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/link/schema.yaml
- allOf:
  - $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/qualifiedValue/schema.yaml
  - anyOf:
    - description: 'The execution unit is a container image. The full schema for this
        branch''s

        `value` property (executionUnitContainer.yaml in the upstream draft) is out
        of

        scope until the "Docker" conformance class is built in this register.'
      type: object
      required:
      - type
      properties:
        type:
          type: string
          enum:
          - docker
          - oci
        value:
          type: object
          additionalProperties: true
    - description: The execution unit is CWL script.
      type: object
      required:
      - mediaType
      properties:
        mediaType:
          type: string
          enum:
          - application/cwl
        value:
          $ref: https://raw.githubusercontent.com/common-workflow-language/cwl-v1.2/main/json-schema/cwl.yaml
    - description: 'The execution unit is not Docker/OCI or CWL and cannot be properly
        described via

        the "mediaType" property of a qualified value using an RFC 2046 media type
        (e.g.

        an "R" or "Python" script). In this case a community-defined or custom token
        may

        be used with the "type" property.'
      type: object
      required:
      - type
      properties:
        type:
          type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitBase/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitBase/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/executionUnitBase`

