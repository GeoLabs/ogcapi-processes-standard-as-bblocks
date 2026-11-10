
# Additional API Building Blocks (Clause)

`ogc.api.processes.part1.v2.clauses.additionalBuildingBlocks` *v2.0*

Additional API building blocks of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): alternative process descriptions and paths.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The core requirements classes of the OGC API-Processes Standard are designed for the following workflow:

1. Access the list of available processes;
2. Access the description of a specific process;
3. Create an execute JSON request (based on the description) and send it to the server via the HTTP POST method;
4. Process the status info and/or results.

This workflow is useful for generic clients that are implemented against the JSON schemas and paths specified in this Standard. Generic clients can communicate with any server implementing the OGC API — Processes Standard. However, there may be limitations regarding the handling of input and output formats.

The approach described above requires implementers of clients to have knowledge about the standard.

This Standard uses the OpenAPI specification to define the JSON schemas and OpenAPI MAY also be used to describe the physical implementation of the API (see [Clause 7.3](#sec-7.3)). A variety of tools for automatic code generation exist for the OpenAPI specification. This makes it very easy for client and server implementers to work with APIs defined using OpenAPI. However, as the OGC API — Processes Standard defines several JSON schemas and leaves the concrete data types for input and outputs open, the automatic code generation cannot be used to its full extent. To cope with this and thus make the implementation of clients / servers easier for those that are not familiar with OGC (API) Standards, additional alternatives to the [process description](#sec-7.11) and the paths to processes and jobs are permitted.

The following permissions do not affect the mandatory core requirements.

<!-- permission: core/alternative-process-description -->

The alternative-process-description permission allows server implementations to describe a process, such as by defining the request and response body of a POST request to a process endpoint using the OpenAPI specification directly (see this [example](#example-alternative-process-description)).

<!-- permission: core/alternative-process-paths -->

The alternative-process-paths permission allows server implementations to specify alternative paths to processes and jobs.

An example of an OpenAPI document making use of these building blocks is shown in the following:

<div id="example-alternative-process-description"></div>

```yaml
openapi: 3.0.2
info:
  title: Alternative OGC API - Processes
  description: This is an alternative OGC API - Processes
  contact:
    email: you@your-company.com
  license:
    name: Apache 2.0
    url: http://www.apache.org/licenses/LICENSE-2.0.html
  version: 1.0.0
paths:
  /buffer:
    post:
      summary: execute buffer process
      operationId: executeBuffer
      requestBody:
        description: buffer inputs
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/bufferExecute'
      responses:
        "200":
          description: buffer created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/bufferResult'
        "400":
          description: invalid input
components:
  schemas:
    bufferExecute:
      required:
        - data
        - width
      type: object
      properties:
        data:
          maxItems: 10
          minItems: 1
          type: array
          description: this is possible to provide the abstract in here
          items:
            oneOf:
              - type: string
                format: application/geo+json
              - type: string
                format: application/gml+xml
        width:
          maximum: 100
          minimum: 1
          type: integer
          default: 20
    bufferResult:
      type: object
      properties:
        outputs:
          type: array
          items:
            oneOf:
              - type: string
                format: application/geo+json
              - type: string
                format: application/gml+xml
```

**Listing 78**

The goals of these additional API building blocks are:

- Enabling a more seamless integration of this API with other OGC API standards and
- Enabling the use of tools to auto-generate clients / servers from the API description.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/clauses/additionalBuildingBlocks`

