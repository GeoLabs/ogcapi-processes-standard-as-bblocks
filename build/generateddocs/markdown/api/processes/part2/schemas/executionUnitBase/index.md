
# Execution unit (single) (Schema)

`ogc.api.processes.part2.schemas.executionUnitBase` *v1.0.0*

One execution unit: a link, or a qualified value holding a container image, a CWL document or a custom type.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

One execution unit: a link, or a qualified value holding a container image, a CWL document or a custom type.

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- The draft refers to `../cwl/cwl.yaml`, which it does not include. This block uses the CWL v1.2 schema URL that the draft gives in a comment.
- As written in the draft, the third `anyOf` branch accepts any `type`, so this schema does not reject an invalid Docker `value`. Validate such a value against `ogc.api.processes.part2.schemas.executionUnitContainer`.

## Schema

```yaml
oneOf:
- $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/link/schema.yaml
- allOf:
  - $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/qualifiedValue/schema.yaml
  - anyOf:
    - description: The execute unit is a container image.
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
          $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnitContainer/schema.yaml
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
    - description: "The execution unit is not Docker/OCI or CWL and cannot be properly\ndescribed
        via the \"mediaType\" property of a qualified value \nusing an RFC 2046 media
        type (e.g. an \"R\" or \"Python\" script).\nIn this case a community-defined
        or custom token may be used\nwith the \"type\" property."
      type: object
      required:
      - type
      properties:
        type:
          type: string
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.executionUnitBase
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

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

