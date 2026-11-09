
# OGC Application Package (Schema)

`ogc.api.processes.part2.schemas.ogcapppkg` *v1.0.0*

Schema of an OGC Application Package document (Requirement /req/ogcapppkg/schema).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Schema of an OGC Application Package document (Requirement /req/ogcapppkg/schema).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

The `docker-example` test is the example from the draft with a top-level `title` added. This block inherits a JSON-LD context that maps no other top-level property, and the build rejects an empty RDF output.

## Schema

```yaml
type: object
required:
- executionUnit
properties:
  processDescription:
    type: object
    required:
    - process
    properties:
      process:
        $ref: https://geolabs.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/process/schema.yaml
  executionUnit:
    $ref: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/executionUnit/schema.yaml
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.ogcapppkg
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/ogcapppkg/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/ogcapppkg/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "title": "dct:title",
    "description": "dct:description",
    "keywords": "proc:keywords",
    "nullable": "proc:nullable",
    "type": "proc:type",
    "$ref": {
      "@id": "proc:ref",
      "@type": "@id"
    },
    "default": {
      "@id": "proc:default",
      "@type": "@json"
    },
    "enum": {
      "@id": "proc:enum",
      "@container": "@set"
    },
    "minOccurs": "proc:minOccurs",
    "maxOccurs": "proc:maxOccurs",
    "dct": "http://purl.org/dc/terms/",
    "proc": "https://w3id.org/ogc/api/processes/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/ogcapppkg/context.jsonld)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/ogcapppkg`

