
# OGC Process Description (Requirements-class)

`ogc.api.processes.part1.requirements.ogcProcessDescription` *v2.0*

Requirements class “OGC Process Description” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): a JSON information model describing the interface of a process.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The following section describes the `OGC Process Description` Requirements Class.

# Overview

<!-- requirements-class -->

The OGC process description is an information model that may be used to specify the interface of a process. This model is an evolution of the process description model originally defined in the [OGC WPS 2.0.2 Interface Standard](https://docs.opengeospatial.org/is/14-065/14-065.html) but also includes elements of the [OpenAPI Specification](https://spec.openapis.org/oas/v3.0.3). Specifically, this process description languages uses [JSON Schema](https://json-schema.org/draft/2020-12/json-schema-core.html) fragments to define the input and output parameters of a process. As such, this process description provides a bridge from legacy WPS implementations to implementing and using the Standards as defined as part of OGC API Framework.

**NOTE:** The use of other schema languages for describing the interface to a process is permitted but is outside the scope of this Standards. A description of how other schema languages would be used to describe the interface of a process would need to be described in a new conformance class added to this Standard or in a new Part of the OGC API — Processes suite of standards.

The process description support specifying the following information:

- An identifier for the process

- Descriptive metadata about the process:

  - A title
  - A narrative description of the process
  - Keywords that can be associated with the process
  - References to additional metadata

- A description of each process input specified using a [JSON Schema](https://json-schema.org/draft/2020-12/json-schema-core.html) fragment.

- A description of each process output specified using a [JSON Schema](https://json-schema.org/draft/2020-12/json-schema-core.html) fragment.

- A job control specification that indicates whether the process can be invoked synchronously, asynchronously, or either.

- An output transmission specification that indicates how the results of a process are retrieved; either by value or by reference

- A section for additional parameters that are intended for communities of use to extend the process description as required.

The following clause defines a JSON-encoding of the OGC process description.

# OGC process description

<!-- requirement: ogc-process-description/json-encoding -->

<!-- requirement: ogc-process-description/links -->

<!-- recommendation: ogc-process-description/process-links -->

<div id="process_description_schema"></div>

```yaml
allOf:
  - $ref: "processSummary.yaml"
  - type: object
    properties:
      inputs:
        additionalProperties:
          $ref: "inputDescription.yaml"
      outputs:
        additionalProperties:
          $ref: "outputDescription.yaml"
```

**Listing 28 — Schema for a process**

**NOTE:** This schema can also be obtained from [`process.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/process.yaml)

(see also [`processSummary.yaml`](#schema-processSummary))

The schema imports the elements from the [process summary](#schema-processSummary) and specifies an object for the definition of process inputs and another object for the definition of process outputs.

# Describing a process input

## Overview

<!-- requirement: ogc-process-description/inputs-def -->

<div id="process-input-schema"></div>

```yaml
allOf:
  - $ref: "descriptionType.yaml"
  - $ref: "dataClasses.yaml"
  - $ref: "dataAccessAPIs.yaml"
  - $ref: "executionUnitRequirements.yaml"
  - $ref: "schemaAndOccurrences.yaml"
  - type: object
    properties:
      valuePassing:
        type: array
        items:
           type: string
           enum:
             - "byValue"
             - "byReference"
        default: ["byValue","byReference"]
```

**Listing 29 — Schema for describing a process input**

**NOTE 1:** This schema can also be obtained from [`inputDescription.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/inputDescription.yaml)

```yaml
description: |-
  Profiling requirements that the specified value, link, collection reference, selected output, or input/output
  definition must meet or adapt to, depending on context, in order to make it adequate for the process execution.
  These requirements are represented as URIs or safe CURIEs providing resolvable profiles applicable to the context.
  They directly corresponds to link references that can be employed for *Content Negotiation by Profile*.
type: object
properties:
  dataClasses:
    type: array
    items:
      anyOf:
        - description: "URI to a registered profile entity."
          type: string
          format: uri
        - $ref: "safeCurie.yaml"
```

**Listing 30 — Schema for the "dataClasses" parameter**

**NOTE 2:** This schema can also be obtained from [`dataClasses.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/dataClasses.yaml)

```yaml
type: object
properties:
  dataAccessAPIs:
    type: array
    items:
      $ref: "apis.yaml"
```

**Listing 31 — Schema for the "dataAccessAPIs" parameter**

**NOTE 3:** This schema can also be obtained from [`dataAccessApis.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/dataAccessAPIs.yaml)

```yaml
type: object
properties:
  executionUnitRequirements:
    type: object
    properties:
      remote-access:
        type: boolean
      staging:
        type: string
        enum:
          - local-file
          - remote-access
```

**Listing 32 — Schema for the "executionUnitRequirements" parameter**

**NOTE 4:** This schema can also be obtained from [`executionUnitRequirements.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/executionUnitRequirements.yaml)

(see also: [`descriptionType.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/descriptionType.yaml)).

## Data classes

One common input type that a process might accept is a [feature collection](https://docs.ogc.org/is/17-069r4/17-069r4.html#_collection_) indicating that the process will operate over the items of the collection. This implies that the process will have certain expectations about the structure of the collection with regard to which properties the collection contains, their types, etc. To properly handle any arbitrary input collection, a process would need to inspect the structure of the collection to ensure that all the expected properties with the expected schemas and semantics are present. To alleviate the server from having to perform such a tedious, and perhaps computationally expensive, validation step this Standard introduces the concept of the *Data Class* via the `dataClasses` parameter.

<!-- requirement: ogc-process-description/data-classes -->

Two data resources tagged with the same data class URI value can be assumed to each contain all the properties defined by the data class. This equivalence enables a server to quickly validate that an input data resource meets the server’s expectations in terms of the properties available for processing simply by comparing data class URI values. If the data class URI of the input data resource matches at least one of the data class URIs specified in the description of the process input (via the `dataClasses` parameter) then the server can assume that the process can operate on that data resource.

**NOTE 1:** Care should be taken when tagging data resources with a data class URI. Both the schema and the semantics of each property in the data class must match the corresponding properties of the data resource. Consider two data resources that both contain fields `a` and `b` with the same data types but differ in, for example, units of measure. In this case, these two data resources should not be tagged with the same data class URI. While the schemas of `a` and `b` in the two data resources are the same, the semantics are clearly different.

The `dataClasses` parameter is an array allowing process inputs to be described that can handle joint association of data classes. As long as the data class URIs associated with an input data resource matches all of the data class URIs listed in the `dataClasses` array, the server can assume that the process can operate on that input data process. The `dataClasses` URIs indicate the semantic contracts that the process expects the input data resource to satisfy.

The `dataClasses` parameter can also be used when describing [process outputs](#sec-9.4) and indicates that the generated output conforms to the schema requirements of the data class. This allows, for example, for a simple determination of whether the output of one process is suitable as an input to another process.

If a data structure needs to fulfill an “*any of contract*” conformance (e.g., either property *fenceSize* or *fenceWidth* must be provided), then a `dataClasses` URI representing that conditional requirement should encode it as such (i.e., similar to a `anyOf` in JSON schema). At the `dataClasses` level, all URIs are unconditionally required. Furthermore, `dataClasses` URIs have an additive behavior. For example, one URI might require a *fenceWidth* property to exist, while another could require measurements to be in meters. The resulting data would conform only if it is simultaneously providing a *fenceWidth* in meters.

This clause started by introducing the concept of the *Data Class* in relation to a [feature collection](https://docs.ogc.org/is/17-069r4/17-069r4.html#_collection_) but the concept is a general one applying to any number of data resources such as feature collections, coverages, styles, etc. For example, a specific data class might be defined to include a geometry property *fenceLine* of type *polygon*. Thus, any input feature collection tagged with this data class’s URI can be expected to include a *fenceLine* property and its type can be assumed to be *polygon*. Similarly, a data class could be defined that identifies a set of bands in a coverage, say R, G, B and NIR. Any coverages tagged with this data class’s URI can thus be assumed to contain these bands. The *Data Class* concept is also independent of the encoding used for the data resource. So, applying data class validation applies equally to feature collections encoded as GeoJSON documents as it does to feature collection formats such as Shape files. Similarly, the concept also extends beyond “*collections*”. A data class asserting a *fenceLine* field requirement could be encoded in by a single GeoTiff raster band, a GeoJSON Polygon, a column in a GeoParquet structure, or a plain CSV header. Finally, the *Data Class* concept is independent of whether data resource values are passed to a process by-value or by-reference. In either case the server goes through the same procedure (i.e. comparing data class URIs) to determine whether a specific input value is suitable for processing as per the process description.

**NOTE 2:**

1. A data resource tagged with a specific data class will contain all the properties defined for that class but may also contain additional properties that are not members of the class. A process expecting an input value of a particular data class value would simply ignore these extraneous properties, unless one of the `dataClasses` URI explicitly requires a strict “*no additional properties*” requirement for it to be valid.
2. In order for the *Data Class* concept to be most effective a registry akin to that found at [Schema.org](https://schema.org) would need to be created and maintained. The [OGC Definitions Service](https://defs.opengis.net/prez/) is likely the best place to define and manage *Data Class* URIs.
3. The `dataClasses` URIs can be employed for [[con-neg-by-profile]](#sec-7.7) when describing data or accessing it from locations that support various representations of the contents being requested. Their content negotiation might be further constrained when combining them with specific [Schema](#sec-9.3.4) definitions, media-types and [Format](#format-key-values) requirements which could impose further data prerequisites depending on their specific values (e.g., `application/gml+xml; version=3.2` or `geojson-geometry` would already impose minimal contains by themselves).
4. Conceptually, `dataClasses` are equivalent to [`prof:Profile`](https://www.w3.org/TR/dx-prof/#Class:Profile) ([W3C Profile](#w3cProfile)) and its associated conformance requirements.

## Data access APIs

If a server supports [collection input](#bb-ogc-api-processes-part1-requirements-collectioninput) and/or [collection output](#bb-ogc-api-processes-part1-requirements-collectionoutput), the `dataAccessAPIs` parameters in the process description allows the server to indicate, on a per-input/output basis, which [OGC API data access mechanism(s)](#sec-4.1.10) are supported for providing input values to the process or retrieving output values from the process.

<!-- requirement: ogc-process-description/data-access-apis -->

<!-- permission: ogc-process-description/extend-data-access-apis-values -->

## Schema

<!-- requirement: ogc-process-description/input-def -->

<!-- requirement: ogc-process-description/input-multiple-types -->

The following JSON Schema fragment illustrates how to define an input that allows multiple types. In this case, the `imageInput` input can be one of a couple of image media types.

```json
{
  "imageInput": {
    "schema": {
      "oneOf": [
        {
          "type": "string",
          "contentEncoding": "binary",
          "contentMediaType": "image/tiff; application=geotiff"
        },
        {
          "type": "string",
          "contentEncoding": "binary",
          "contentMediaType": "image/jp2"
        }
      ]
    }
  }
}
```

**Listing 33 — Input of multiple types example**

<!-- recommendation: ogc-process-description/format-key -->

Processes that perform geospatial processing can be expected to have geometric and feature input types. In JSON, geometries, features, and feature collections are commonly encoded using [GeoJSON](https://datatracker.ietf.org/doc/html/rfc7946). Rather the requiring processes descriptions to embed or reference the full schemas for [GeoJSON](https://datatracker.ietf.org/doc/html/rfc7946) geometries, features or feature collections, this Standard defines a common set of convenience tokens that can be used instead.

The [JSON Schema specification](#jsonschemavalidation) defines a [set of values](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7) for the `format` key. This Standard extends this list by defining the following additional key values for use specifically in OGC process descriptions.

**Table 11 — Additional values for the JSON schema format key for OGC Process Description**

<div id="format-key-values"></div>

| Key value | Short code | Description |
|---|---|---|
| [https://www.opengis.net/def/format/ogcapi-processes/0/geojson-feature-collection](https://www.opengis.net/def/format/ogcapi-processes/0/geojson-feature-collection) | `geojson-feature-collection` | Indicates that the value is an instance of a GeoJSON feature collection<br>[(featureCollectionGeoJSON.yaml)](https://schemas.opengis.net/ogcapi/features/part1/1.0/openapi/schemas/featureCollectionGeoJSON.yaml)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/geojson-feature](https://www.opengis.net/def/format/ogcapi-processes/0/geojson-feature) | `geojson-feature` | Indicates that the value is an instance of a GeoJSON feature<br>[(featureGeoJSON.yaml)](https://schemas.opengis.net/ogcapi/features/part1/1.0/openapi/schemas/featureGeoJSON.yaml)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/geojson-geometry](https://www.opengis.net/def/format/ogcapi-processes/0/geojson-geometry) | `geojson-geometry` | Indicates that the value is an instance of a GeoJSON geometry<br>[(geometryGeoJSON.yaml)](https://schemas.opengis.net/ogcapi/features/part1/1.0/openapi/schemas/geometryGeoJSON.yaml)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/ogc-bbox](https://www.opengis.net/def/format/ogcapi-processes/0/ogc-bbox) | `ogc-bbox` | Indicates that the value is an instance of an OGC bounding box<br>[(bbox.yaml)](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/bbox.yaml)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/epsg-code](https://www.opengis.net/def/format/ogcapi-processes/0/epsg-code) | `epsg-code` | Indicates that the string value is a code from the<br>[EPSG registry](https://epsg.io/)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/wkt2-definition](https://www.opengis.net/def/format/ogcapi-processes/0/wkt2-definition) | `wkt2-definition` | Indicates that the string value is a<br>[well-known text representation of a coordinate reference system](https://docs.ogc.org/is/18-010r11/18-010r11.pdf)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/cql2-text-filter](https://www.opengis.net/def/format/ogcapi-processes/0/cql2-text-filter) | `cql2-text` | Indicates that the string value is a filter expression encoded using the text representation of the<br>[Common Query Language (CQL2)](https://docs.ogc.org/is/21-065r2/21-065r2.html)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/cql2-json-filter](https://www.opengis.net/def/format/ogcapi-processes/0/cql2-json-filter) | `cql2-json` | Indicates that the string value is a filter expression encoded using the JSON representation of the<br>[Common Query Language (CQL2)](https://docs.ogc.org/is/21-065r2/21-065r2.html)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/collection-id](https://www.opengis.net/def/format/ogcapi-processes/0/collection-id) | `collection-id` | Indicates that the string value is a<br>[collection identifier](https://docs.ogc.org/DRAFTS/20-024.html#collection-description)<br>(e.g. a feature collection identifier). |
| [https://www.opengis.net/def/format/ogcapi-processes/0/stac-collection](https://www.opengis.net/def/format/ogcapi-processes/0/stac-collection) | `stac-collection` | Indicates that the value is an instance of a<br>[STAC collection](https://github.com/radiantearth/stac-spec/blob/v1.1.0/collection-spec/collection-spec.md)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/stac-catalog](https://www.opengis.net/def/format/ogcapi-processes/0/stac-catalog) | `stac-catalog` | Indicates that the value is an instance of a<br>[STAC catalog](https://github.com/radiantearth/stac-spec/blob/v1.1.0/catalog-spec/catalog-spec.md)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/stac-item-collection](https://www.opengis.net/def/format/ogcapi-processes/0/stac-item-collection) | `stac-item-collection` | Indicates that the value is a<br>[STAC ItemCollection](https://github.com/radiantearth/stac-api-spec/blob/release/v1.0.0/fragments/itemcollection/README.md)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/stac-item](https://www.opengis.net/def/format/ogcapi-processes/0/stac-item) | `stac-item` | Indicates that the value is an instance of a<br>[STAC item](https://github.com/radiantearth/stac-spec/blob/v1.1.0/item-spec/item-spec.md)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/stac](https://www.opengis.net/def/format/ogcapi-processes/0/stac) | `stac` | Indicates that the value is an instance of any of the STAC types listed above (i.e. one of<br>`stac-collection`<br>,<br>`stac-catalog`<br>,<br>`stac-item-collection`<br>, or<br>`stac-item`<br>). |
| [https://www.opengis.net/def/format/ogcapi-processes/0/ogc-feature-collection](https://www.opengis.net/def/format/ogcapi-processes/0/ogc-feature-collection) | `ogc-feature-collection` | Indicates that the value is an instance of an<br>[OGC feature collection](https://docs.ogc.org/is/17-069r4/17-069r4.html#_collection_)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/ogc-coverage-collection](https://www.opengis.net/def/format/ogcapi-processes/0/ogc-coverage-collection) | `ogc-coverage-collection` | Indicates that the value is an instance of an<br>[OGC coverage collection](https://docs.ogc.org/DRAFTS/19-087.html#_extended_collection_description_response_collectionscollectionid)<br>. |
| [https://www.opengis.net/def/format/ogcapi-processes/0/ogc-dggs-collection](https://www.opengis.net/def/format/ogcapi-processes/0/ogc-dggs-collection) | `ogc-dggs-collection` | Indicates that the value is an instance of an<br>[OGC Discreate Global Grid System collection](https://docs.ogc.org/DRAFTS/19-087.html#_extended_collection_description_response_collectionscollectionid)<br>. |

**NOTE 1:** This list of values has been submitted to the [OGC Naming Authority](https://www.ogc.org/projects/groups/ogcnasc) for registration in their definition server.

**NOTE 2:** Other encodings for geometric, feature and feature collection typed inputs/outputs are allowed but are not described in this Standard.

<!-- recommendation: ogc-process-description/format-short-code -->

Situations might arise where communities of interest wish to extend this list of values for their own purposes.

<!-- recommendation: ogc-process-description/format-value-registration -->

The following JSON Schema fragment illustrates the use of the `format` key to include a semantic hint to a process input that is of a geometric type.

```json
{
  "geometryInput": {
    "title": "Geometry input",
    "description": "This is an example of a geometry input.  In this case the geometry can be expressed as a GML of GeoJSON geometry.",
    "minOccurs": 2,
    "maxOccurs": 5,
    "schema": {
      "oneOf": [
        {
          "type": "string",
          "contentMediaType": "application/gml+xml; version=3.2",
          "contentSchema": "https://schemas.opengis.net/gml/3.2.1/geometryBasic2d.xsd"
        },
        {
          "format": "geojson-geometry"
        }
      ]
    }
  }
}
```

**Listing 34 — Example of semantic hints using the format key**

## Cardinality

### Overview

The cardinality on an input is specified using the `minOccurs` and `maxOccurs` parameters from the input’s definition in the [process description](#sec-7.11). The default values of `minOccurs` and `maxOccurs` are 1 indicating that a single input of the corresponding name must be specified in an execute request. The following table covers the various combinations of `minOccurs` and `maxOccurs` values.

**Table 12 — Cardinality rules for process inputs.**

<div id="cardinality_rules"></div>

| minOccurs | maxOccurs | Interpretation | Example |
|---|---|---|---|
| 0 | 0 | Not Allowed |  |
| 0 | 1 | A single input value<br>**may**<br>be optionally specified. | `"input": {value}` |
| 1 | 1 | A single input value<br>**must**<br>be specified. | `"input": {value}` |
| 1 | N | At least 1 input value<br>**must**<br>be specified.<br>Regardless of the number of input values provided, those values<br>**must**<br>be encoded using an array. | `"input": [{value}]`<br>OR<br>`"input": [{value1},…,{valueN}]` |
| M | N | All values provided<br>**must**<br>be encoded using an array. | `"input": [{value1},…,{valueM}]`<br>OR<br>`"input": [{value1},…,{valueM},…,{valueN}]` |

**NOTE:** The tokens `{value}`, `{value1}`, `{valueN}` or `{valueM}` represent values of the type expected for the input according to its definition. This can include array values.

### Interaction of minOccurs/maxOccurs and minItems/maxItems

The `schema` member of the [input definition](#process-input-schema) in the [process description](#sec-7.11) defines the schema of a single instance of an input. If the input happens to be an array, then the `minItems` and `maxItems` properties may be used to define the limits of the array. The use of `minItems` and `maxItems` in the definition of the input does not affect how `minOccurs` and `maxOccurs` are interpreted and the same [cardinality rules](#cardinality_rules) apply.

Consider the following definitions of an input named “input”.

**Table 13 — Schema examples for cardinality**

| Example Schema | Examples instances |
|---|---|
| <p></p><pre id="row1-example">inputs:<br>  input:<br>    schema:<br>      type: array<br>      maxItems: 2<br>      items:<br>        type: string</pre> <p>In this case the schema of an input value is defined as an array and so will always be encoded as an array in an execute request.</p> | <p></p><pre>{"input": ["value1"]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": ["value1","value2"]}</pre> |
| <p></p><pre>inputs:<br>  input:<br>    maxOccurs: 2<br>    schema:<br>      type: string</pre> <p>In this case, the schema of the input is defined as a plain string with a cardinality of 2.  Inputs with cardinalities of greater than 1 are encoded as arrays in an execute request.  This situation is equivalently encoded to the <a href="#row1-example">previous row</a>.<br> Servers, however, being internally aware of the definition of each input, can disambiguate the input values accordingly (treating the values in this example as string values and the values in the  <a href="#row1-example">above example</a> as arrays of values).</p> | <p></p><pre>{"input": ["value1"]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": ["value1","value2"]}</pre> |
| <p></p><pre>inputs:<br>  input:<br>    maxOccurs: 2<br>    schema:<br>      type: array<br>      maxItems: 2<br>      items:<br>        type: string</pre> <p>In this case we have an input with cardinality greater than 1 but that has values that themselves are defined as arrays.  Since inputs with cardinality greater than 1 are encoded as arrays in an execute request, the result is that the inputs are encoded as arrays of arrays.</p> | <p></p><pre>{"input": [["value1"]]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": [["value1","value2"]]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": [["value1"],["value2"]]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": [["value1","value3"],["value2"]]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": [["value1"],["value2","value3"]]}</pre> <p><strong>or</strong></p> <p></p><pre>{"input": [["value1","value4"],["value2","value3"]]}</pre> |

## Value passing

<!-- requirement: ogc-process-description/value-passing -->

<!-- permission: ogc-process-description/value-passing -->

## Execution unit requirements

The `executionUnitRequirements` parameter is used to specify runtime requirements for the corresponding input. For example, the `executionUnitRequirements` parameter would be used to specify that an input value needs to be staged locally for the execution unit.

<!-- requirement: ogc-process-description/execution-unit-requirements -->

# Describing a process output

## Overview

<!-- requirement: ogc-process-description/outputs-def -->

<!-- requirement: ogc-process-description/output-def -->

<!-- requirement: ogc-process-description/output-multiple-types -->

```yaml
allOf:
  - $ref: "descriptionType.yaml"
  - $ref: "dataClasses.yaml"
  - $ref: "dataAccessAPIs.yaml"
  - $ref: "schemaAndOccurrences.yaml"
```

**Listing 48 — Schema for describing a process output**

**NOTE:** This schema can also be obtained from [`outputDescription.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/outputDescription.yaml)

(see also: [`descriptionType.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/descriptionType.yaml)).

## Data classes parameter

See [Clause 9.3.2](#sec-9.3.2).

## Data access APIs

See [Clause 9.3.3](#sec-9.3.3).

# Example

The following URL is an example of retrieving a [process description](#sec-7.11) from the `/processes/{processID}` endpoint.

```
https://processing.example.org/processes/EchoProcess
```

**Listing 49**

The description of the example `EchoProcess` process might be:

```json
{
  "id": "EchoProcess",
  "title": "Echo Process",
  "description": "This process accepts and number of input and simple echoes each input as an output.",
  "version": "1.0.0",
  "jobControlOptions": [
    "async-execute",
    "sync-execute"
  ],
  "inputs": {
    "stringInput": {
      "title": "String Literal Input Example",
      "description": "This is an example of a STRING literal input.",
      "schema": {
        "type": "string",
        "enum": [
          "Value1",
          "Value2",
          "Value3"
        ]
      }
    },
    "measureInput": {
      "title": "Numerical Value with UOM Example",
      "description": "This is an example of a NUMERIC literal with an associated unit of measure.",
      "schema": {
        "type": "object",
        "required": [
          "measurement",
          "uom"
        ],
        "properties": {
          "measurement": {
            "type": "number"
          },
          "uom": {
            "type": "string"
          },
          "reference": {
            "type": "string",
            "format": "uri"
          }
        }
      }
    },
    "dateInput": {
      "title": "Date Literal Input Example",
      "description": "This is an example of a DATE literal input.",
      "schema": {
        "type": "string",
        "format": "date-time"
      }
    },
    "doubleInput": {
      "title": "Bounded Double Literal Input Example",
      "description": "This is an example of a DOUBLE literal input that is bounded between a value greater than 0 and 10.  The default value is 5.",
      "schema": {
        "type": "number",
        "format": "double",
        "minimum": 0,
        "maximum": 10,
        "default": 5,
        "exclusiveMinimum": true
      }
    },
    "arrayInput": {
      "title": "Array Input Example",
      "description": "This is an example of a single process input that is an array of values.  In this case, the input array would be interpreted as a single value and not as individual inputs.",
      "schema": {
        "type": "array",
        "minItems": 2,
        "maxItems": 10,
        "items": {
          "type": "integer"
        }
      }
    },
    "complexObjectInput": {
      "title": "Complex Object Input Example",
      "description": "This is an example of a complex object input.",
      "schema": {
        "type": "object",
        "required": [
          "property1",
          "property5"
        ],
        "properties": {
          "property1": {
            "type": "string"
          },
          "property2": {
            "type": "string",
            "format": "uri"
          },
          "property3": {
            "type": "number"
          },
          "property4": {
            "type": "string",
            "format": "date-time"
          },
          "property5": {
            "type": "boolean"
          }
        }
      }
    },
    "geometryInput": {
      "title": "Geometry input",
      "description": "This is an example of a geometry input.  In this case the geometry can be expressed as a GML of GeoJSON geometry.",
      "minOccurs": 2,
      "maxOccurs": 5,
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentMediaType": "application/gml+xml; version=3.2",
            "contentSchema": "http://schemas.opengis.net/gml/3.2.1/geometryBasic2d.xsd"
          },
          {
            "format": "geojson-geometry"
          }
        ]
      }
    },
    "boundingBoxInput": {
      "title": "Bounding Box Input Example",
      "description": "This is an example of a BBOX literal input.",
      "schema": {
        "allOf": [
          {
            "format": "ogc-bbox"
          },
          {
            "$ref": "bbox.json"
          }
        ]
      }
    },
    "imagesInput": {
      "title": "Inline Images Value Input",
      "description": "This is an example of an image input.  In this case, the input is an array of up to 150 images that might, for example, be a set of tiles.  The oneOf[] conditional is used to indicate the acceptable image content types; GeoTIFF and JPEG 2000 in this case.  Each input image in the input array can be included inline in the execute request as a base64-encoded string or referenced using the link.yaml schema.  The use of a base64-encoded string is implied by the specification and does not need to be specified in the definition of the input.",
	   "minOccurs": 1,
	   "maxOccurs": 150,
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentEncoding": "binary",
            "contentMediaType": "image/tiff; application=geotiff"
          },
          {
            "type": "string",
            "contentEncoding": "binary",
            "contentMediaType": "image/jp2"
          }
        ]
      },
      "dataAccessApis": [
        "ogc-api-coverage",
        "stac-api"
      }
    },
    "featureCollectionInput": {
      "title": "Feature Collection Input Example.",
      "description": "This is an example of an input that is a feature collection that can be encoded in one of three ways: as a GeoJSON feature collection, as a GML feature collection retrieved from a WFS or as a KML document.",
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentMediaType": "application/gml+xml; version=3.2"
          },
          {
            "type": "string",
            "contentSchema": "https://schemas.opengis.net/kml/2.3/ogckml23.xsd",
            "contentMediaType": "application/vnd.google-earth.kml+xml"
          },
          {
            "allOf": [
              {
                "format": "geojson-feature-collection"
              },
              {
                "$ref": "https://geojson.org/schema/FeatureCollection.json"
              }
            ]
          }
        ]
      },
      "dataAccessApis": [
        "ogc-api-features"
      ]
    }
  },
  "outputs": {
    "stringOutput": {
      "schema": {
        "type": "string",
        "enum": [
          "Value1",
          "Value2",
          "Value3"
        ]
      }
    },
    "measureOutput": {
      "schema": {
        "type": "object",
        "required": [
          "measurement",
          "uom"
        ],
        "properties": {
          "measurement": {
            "type": "number"
          },
          "uom": {
            "type": "string"
          },
          "reference": {
            "type": "string",
            "format": "uri"
          }
        }
      }
    },
    "dateOutput": {
      "schema": {
        "type": "string",
        "format": "date-time"
      }
    },
    "doubleOutput": {
      "schema": {
        "type": "number",
        "format": "double",
        "minimum": 0,
        "maximum": 10,
        "default": 5,
        "exclusiveMinimum": true
      }
    },
    "arrayOutput": {
      "schema": {
        "type": "array",
        "minItems": 2,
        "maxItems": 10,
        "items": {
          "type": "integer"
        }
      }
    },
    "complexObjectOutput": {
      "schema": {
        "type": "object",
        "required": [
          "property1",
          "property5"
        ],
        "properties": {
          "property1": {
            "type": "string"
          },
          "property2": {
            "type": "string",
            "format": "uri"
          },
          "property3": {
            "type": "number"
          },
          "property4": {
            "type": "string",
            "format": "date-time"
          },
          "property5": {
            "type": "boolean"
          }
        }
      }
    },
    "geometryOutput": {
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentMediaType": "application/gml+xml",
            "contentSchema": "http://schemas.opengis.net/gml/3.2.1/geometryBasic2d.xsd"
          },
          {
            "allOf": [
              {
                "format": "geojson-geometry"
              },
              {
                "$ref": "https://geojson.org/schema/Geometry.json"
              }
            ]
          }
        ]
      }
    },
    "boundingBoxOutput": {
      "schema": {
        "allOf": [
           {
             "format": "ogc-bbox"
           },
           {
             "$ref": "bbox.json"
           }
        ]
      }
    },
    "imagesOutput": {
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentEncoding": "binary",
            "contentMediaType": "image/tiff; application=geotiff"
          },
          {
            "type": "string",
            "contentEncoding": "binary",
            "contentMediaType": "image/jp2"
          }
        ]
      }
    },
    "featureCollectionOutput": {
      "schema": {
        "oneOf": [
          {
            "type": "string",
            "contentMediaType": "application/gml+xml; version=3.2"
          },
          {
            "type": "string",
            "contentMediaType": "application/vnd.google-earth.kml+xml",
            "contentSchema": "https://schemas.opengis.net/kml/2.3/ogckml23.xsd"
          },
          {
            "allOf": [
              {
                "format": "geojson-feature-collection"
              },
              {
                "$ref": "https://geojson.org/schema/FeatureCollection.json"
              }
            ]
          }
        ]
      }
    }
  },
  "links": [
    {
      "href": "https://processing.example.org/oapi-p/processes/EchoProcess/execution",
      "rel": "http://www.opengis.net/def/rel/ogc/1.0/execute",
      "title": "Execute endpoint"
    },
    {
      "href": "https://www.opengis.net/def/profile/OGC/0/ogc-process-description",
      "rel": "profile"
    }
  ]
}
```

**Listing 50**

The `EchoProcess` process simply echoes each process input value it is given.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/ogcProcessDescription`

