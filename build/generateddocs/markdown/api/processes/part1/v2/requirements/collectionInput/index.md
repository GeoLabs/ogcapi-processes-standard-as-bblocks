
# Collection Input (Requirements-class)

`ogc.api.processes.part1.v2.requirements.collectionInput` *v2.0*

Requirements class “Collection Input” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): OGC API collections as process inputs.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

The *Collection Input* Requirements Class supports specifying as an input to a process an [OGC API accessible collection](#sec-4.1.1) via using one or more [OGC API data access mechanisms](#sec-4.1.10). Specifically, the processing server acts as a client and fetches values from the [OGC API accessible collection](#sec-4.1.1) using one of the available [OGC API data access mechanisms](#sec-4.1.10) and then feeds the fetched values as input values to the process being executed. The server from which input values are retrieved is referred to as the [*value source server*](#sec-4.1.22).

Unless an implementation also conforms to the [*Remote Collections*](#sec-8.2) conformance class, only [collections](#sec-4.1.1) that are locally accessible in the current [OGC API deployment](#sec-4.1.11) are supported.

Unless an implementation also conforms to the [*Local Filtering*](#sec-8.4) conformance class, filtering of values retrieved from an [OGC API accessible collection](#sec-4.1.1) is performed by the [value source server](#sec-4.1.22).

<!-- requirements-class -->

The following requirements describe how an [execute request](#execute-request-body) references an [OGC API accessible collection](#sec-4.1.1) and how an implementation requests data from that collection to use as input to a process.

# Referencing a collection

<!-- requirement: collection-input/referencing -->

<div id="collection-value-schema"></div>

```yaml
allOf:
  - $ref: format.yaml
  - type: object
    required:
      - collection
    properties:
      collection:
        description: |-
           The URI of the OGC API collection that should be accessed to provide
           input values from the corresponding process input.  The server
           offering this collection is referred to as the "value source server".
        anyOf:
          - type: string
            description: |-
              Collection identifier for a collection available at `{root}/collections/{collectionID}`, where `{root}` represents the landing page
              of the process using the collection as an input (for the top-level process, that is the landing page of the process execution endpoint
              to which the execution request is posted), or the landing page of the document being retrieved in the case of an output.
              If the `collection` string includes a `/`, it must be interpreted as a URI reference rather than as a collection ID.
          - type: string
            description: |-
               The URI of an OGC API collection.
               If a relative URI reference is used, the Base URI is defined as such:
               - For a Collection value received as input to a process, the Base URI is defined as the URI of the description
                 (`{root}/processes/{processId}`) of that process, with the receiving process object understood as the Encapsulating Entity as per
                 [RFC 3986 Section 5.1.2](https://datatracker.ietf.org/doc/html/rfc3986#section-5.1.2).
               - For a Collection Output value, the Base URI is defined from the Retrieval URI as as per
                 [RFC 3986 Section 5.1.3](https://datatracker.ietf.org/doc/html/rfc3986#section-5.1.3),
                 for example, `/jobs/{jobId}/results`, `/jobs/{jobId}/results/{outputID}` or `/jobs/{jobId}/results/{outputID}/{N}` depending on the
                 resource being retrieved.
               If a collection string does not contain any `/`, it must not be interpreted as a URI reference, and must instead be resolved as a
               collection identifier. For example, `countries` would resolve to `{root}/collections/countries` rather than `{root}/processes/countries`.
            format: uri-reference
      bbox:
        description: |-
          Only resources that have a geometry that intersects the bounding box
          are selected.  The bounding box is provided as four or six numbers,
          depending on whether the coordinate reference system includes a
          vertical axis (height or depth):

          * Lower left corner, coordinate axis 1
          * Lower left corner, coordinate axis 2
          * Minimum value, coordinate axis 3 (optional)
          * Upper right corner, coordinate axis 1
          * Upper right corner, coordinate axis 2
          * Maximum value, coordinate axis 3 (optional)

          If the value consists of four numbers, the coordinate reference
          system is WGS84 longitude/latitude
            (http://www.opengis.net/def/crs/OGC/1.3/CRS84)
          unless a different coordinate reference system is specified in the
          parameter `bboxCrs`.

          If the value consists of six numbers, the coordinate reference system
          is WGS84 (http://www.opengis.net/def/crs/OGC/0/CRS84h) longitude/
          latitude/ ellipsoidal height unless a different coordinate reference
          system is specified in the parameter `bboxCrs`.

          For WGS84 longitude/latitude the values are in most cases the sequence
          of minimum longitude, minimum latitude, maximum longitude and maximum
          latitude.  However, in cases where the box spans the antimeridian the
          first value (west-most box edge) is larger than the third value
          (east-most box edge).

          If the vertical axis is included, the third and the sixth number are
          the bottom and the top of the 3-dimensional bounding box.

          If a resource has multiple spatial geometry properties, it is the
          decision of the server whether only a single spatial geometry property
          is used to determine the extent or all relevant geometries.
        type: array
        oneOf:
          - minItems: 4
            maxItems: 4
          - minItems: 6
            maxItems: 6
        items:
          type: number
      bboxCrs:
        description: |-
          Asserts the CRS used for the coordinate values of the `bbox`
          parameter.  The default is WGS 84 or WGS84h depending on whether
          ellipsoidal height is included or not:
            * WGS 84 longitude/latitude [4 numbers]
              (http://www.opengis.net/def/crs/OGC/1.3/CRS84)
            * WGS 84h longitude/latitude/ellipsoidal height [6 numbers]
              (http://www.opengis.net/def/crs/OGC/0/CRS84h_
        type: string
        format: uri
      geometry:
         description: |-
          Only resources that have a geometry that intersects the geometry
          specified using the `geometry` parameter are selected.  The value of
          the `geometry` parameter can be specified using WKT or GeoJSON.
          If a resource has multiple spatial geometry properties, it is the
          decision of the server whether only a single spatial geometry property
          is used to determine the extent or all relevant geometries.
         oneOf:
           - type: string
           - $ref: "https://schemas.opengis.net/ogcapi/features/part1/1.0/openapi/schemas/geometryGeoJSON.yaml"
      geometryCrs:
        description: |-
          Asserts the CRS used for the coordinate values of the `geometry`
          parameter.  The default is WGS 84 or WGS84h depending on whether
          ellipsoidal height is included or not:
            * WGS 84 longitude/latitude [4 numbers]
              (http://www.opengis.net/def/crs/OGC/1.3/CRS84)
            * WGS 84h longitude/latitude/ellipsoidal height [6 numbers]
              (http://www.opengis.net/def/crs/OGC/0/CRS84h_
        type: string
      datetime:
        description: |-
          Either a date-time or an interval, half-bounded or bounded. Date and
          time expressions adhere to RFC 3339. Half-bounded intervals are
          expressed using double-dots.

          Examples:
            * A date-time:
              "2018-02-12T23:20:50Z"
            * A bounded interval:
              "2018-02-12T00:00:00Z/2018-03-18T12:31:12Z"
            * Half-bounded intervals:
              "2018-02-12T00:00:00Z/.." or "../2018-03-18T12:31:12Z"

          Only resources that have a temporal property that intersects the
          value of `datetime` are selected.

          If a resource has multiple temporal properties, it is the decision of
          the server whether only a single temporal property is used to
          determine the extent or all relevant temporal properties.
        type: string
      limit:
        description: |-
          The optional limit parameter limits the number of items that are
          presented in the response document.
          Only items are counted that are on the first level of the collection
          in the response document.  Nested objects contained within the
          explicitly requested items shall not be counted.
        type: integer
        minimum: 1
        maximum: 10000
        default: 10
      crs:
        description: |-
          If the parameter is specified, then the coordinates of all
          geometry-valued properties in the response document are in
          the requested CRS. Otherwise the coordinates are in the default CRS,
          that is http://www.opengis.net/def/crs/OGC/1.3/CRS84 for coordinates
          without height and http://www.opengis.net/def/crs/OGC/0/CRS84h for
          coordinates with ellipsoidal height.
        type: string
        format: uri
      filter:
        description: |-
           A search or filter condition.  This condition determines which
           resources from the OGC API collection are included in the result
           set and are thus passed as values to the corresponding process input.
           The `filter` parameter can be a string where the search condition is
           encoded in some text-based query langauge (e.g. cql2-text) or a
           CQL2 JSON object that encodes the search condition using JSON.
        oneOf:
          - type: string
          - $ref: ../cql2/cql2.yaml
          # - $ref: "https://schemas.opengis.net/cql2/1.0/cql2.json"
      filterCrs:
        description: |-
          Asserts the CRS used for the coordinate values of the `filter`
          parameter.  The default is WGS 84 or WGS 84h depending on whether
          ellispoidal jeight is included with the coordinates or not:
            * WGS 84 longitude/latitude
              (http://www.opengis.net/def/crs/OGC/1.3/CRS84)
            * WGS 84h longitude/latitude/ellipsoidal height
              (http://www.opengis.net/def/crs/OGC/0/CRS84h_
        type: string
        format: uri-reference
      filterLang:
        description: |-
           Indicates the language used to encode a filter expression specified
           using the `filter` parameter. Query languages can include CQL2 text,
           CQL 2 JSON or OGC Filter Encoding (XML).
        type: string
        enum:
        - cql2-text
        - cql2-json
        - fes-xml
      subset:
        description: |-
          Retrieve only part of the data by slicing or trimming along one or
          more axis. For trimming: {axisAbbrev}({low}:{high}) (preserves
          dimensionality). An asterisk (`*`) can be used instead of {low} or
          {high} to indicate the minimum/maximum value. For slicing:
          {axisAbbrev}({value}) (reduces dimensionality).
        type: array
        items:
          type: string
      subsetCrs:
        description: |-
          Asserts the CRS used for the coordinate values of the `subset`
          parameter.  The default is WGS 84 or WGS 84h depending on whether
          ellispoidal height in included with the coordinates or not:
            * WGS 84 longitude/latitude
              (http://www.opengis.net/def/crs/OGC/1.3/CRS84)
            * WGS 84h longitude/latitude/ellipsoidal height
              (http://www.opengis.net/def/crs/OGC/0/CRS84h_
        type: string
      ids:
        description: |-
          The optional ids parameter allows a specific list of resources,
          indicated by their identifiers, to be fetched from the OGC API
          collection. Only resources whose identifier matches one of the
          values listed for this parameter shall appear in the result set.
        type: array
        items:
          type: string
      q:
        description: |-
          The optional q parameter supports keyword searching.  Only resources
          whose text fields contain one or more of the specified search terms
          are selected.  The specific set of text keys/fields/properties of a
          resource to which the q operator is applied is up to the discretion
          of the server.   Implementations should, however, apply the q
          operator to the title, description and keywords keys/fields/properties
          if they exist in the resource.
        type: array
        items:
          type: string
      assets:
        description: |-
          A list of STAC asset tags.
        type: array
        items:
          type: string
      properties:
        description: |-
          A filter that selects resource properties to be included in a
          response document.  The elements in the `properties` parameter can
          be the names of resource properties, aliases for resources properties
          or synthetic properties.  Synthetic properties are properties that
          are computed on the fly and can reference resource property names
          or aliases for resource properties.
        type: array
        items:
          type: string
      aliases:
        description: |-
          A dictionary of aliases that can be used as values for the
          `properties` parameter.  Aliases can be alternative names for
          resource properties or synthetic properties.  Synthetic properties
          are named expressions that are computed at run-time.  Expressions
          for synthetic properties are encoded using some expression language
          and can include references to resource property names or aliases
          for resource properties..
        type: object
        additionalProperties:
          oneOf:
            - type: string
            - type: object
              properties:
                expressionLang:
                  type: string
                  enum:
                  - cql2-text
                  - cql2-json
                expression:
                  oneOf:
                    - type: string
                    - $ref: ../cql2/cql2.yaml
                    #- $ref: "https://schemas.opengis.net/cql2/1.0/cql2.json"
      passThroughParameters:
        description: |-
          Parameters specified in this object are passed through to the value
          source server for processing on that server.  The keys used in this
          object should be identical to query parameters that the value source
          server would recognize.  In the case where the OAProc server supports
          local filtering, the `passThroughParameters` property provides a
          mechanism to force filtering to happen on the value source server.
        type: object
```

**Listing 24 — Schema for the collection parameter**

# Accessing data from a collection

## Overview

The following requirements describe how to access data from an [OGC API accessible collection](#sec-4.1.1) and the ability of an implementation to modify the accessed data by first applying filters, selecting a subset of fields or deriving new fields before providing the data as input to a process.

<!-- requirement: collection-input/collection-access -->

**NOTE:** For [local collections](#sec-4.1.9), the specification is agnostic to how data flows from the [collection](#sec-4.1.9) to the process.

## Filtering

<!-- requirement: collection-input/filtering -->

**NOTE:** The server may also do some intelligent remapping of parameters. For example, if a `bbox` parameter is specified in the execute request, but the [value source server](#sec-4.1.22) only supports the `geometry` parameter, the implementation may convert the bounding box to a 4-point polygon and map the specified `bbox` parameter to the `geometry` parameter supported by the [value source server](#sec-4.1.22).

### Parameter filter

A search or filter condition. This condition determines which resources from the OGC API collection are included in the result set and are thus passed as values to the corresponding process input. The `filter` parameter can be a string where the search condition is encoded in some text-based query language (e.g. cql2-text) or a CQL2 JSON object that encodes the search condition using JSON.

### Parameter filterCrs

Asserts the CRS used for the coordinate values of the `filter` parameter. The default is WGS 84 or WGS 84h depending on whether ellipsoidal height is included with the coordinates or not:

- WGS 84 longitude/latitude ([https://www.opengis.net/def/crs/OGC/1.3/CRS84](https://www.opengis.net/def/crs/OGC/1.3/CRS84))
- WGS 84h longitude/latitude/ellipsoidal height ([https://www.opengis.net/def/crs/OGC/0/CRS84h\_](https://www.opengis.net/def/crs/OGC/0/CRS84h_)

### Parameter filterLang

Indicates the language used to encode a filter expression specified using the `filter` parameter. Query languages can include CQL2 text, CQL 2 JSON or OGC Filter Encoding (XML).

### Parameter bbox

Only resources that have a geometry that intersects the bounding box are selected to be passed as input values to an executing process. If a resource has multiple spatial geometry properties, it is the decision of the value source server whether only a single spatial geometry property is used to determine the extent or all relevant geometries.

### Parameter bboxCrs

Asserts the CRS used for the coordinate values of the `bbox` parameter. The default is WGS 84 or WGS84h depending on whether ellipsoidal height is included or not:

- WGS 84 longitude/latitude [4 numbers] ([https://www.opengis.net/def/crs/OGC/1.3/CRS84](https://www.opengis.net/def/crs/OGC/1.3/CRS84))
- WGS 84h longitude/latitude/ellipsoidal height [6 numbers] ([https://www.opengis.net/def/crs/OGC/0/CRS84h\_](https://www.opengis.net/def/crs/OGC/0/CRS84h_)

### Parameter datetime

Either a date-time or an interval, half-bounded or bounded. Date and time expressions adhere to [IETF RFC 3339](#rfc3339). Half-bounded intervals are expressed using double-dots. Only resources that have a temporal property that intersects the value of `datetime` are selected. If a resource has multiple temporal properties, it is the decision of the server whether only a single temporal property is used to determine the extent or all relevant temporal properties.

### Parameter subset

Retrieve only part of the data by slicing or trimming along one or more axis. For specifying a trim operation: `{axisAbbrev}({low}:{high})` (preserves dimensionality). An asterisk (`*`) can be used instead of `{low}` or `{high}` to indicate the minimum/maximum value. For expression a slice operation: `{axisAbbrev}({value})` (reduces dimensionality).

### Parameter subsetCrs

Asserts the CRS used for the coordinate values of the `subset` parameter. The default is WGS 84 or WGS 84h depending on whether ellipsoidal height in included with the coordinates or not:

- WGS 84 longitude/latitude ([`https://www.opengis.net/def/crs/OGC/1.3/CRS84`](https://www.opengis.net/def/crs/OGC/1.3/CRS84))
- WGS 84h longitude/latitude/ellipsoidal height ([`https://www.opengis.net/def/crs/OGC/0/CRS84h`](https://www.opengis.net/def/crs/OGC/0/CRS84h))

### Parameter geometry

Only resources that have a geometry that intersects the geometry specified using the `geometry` parameter are selected. The value of the `geometry` parameter can be specified using Well Known Text (WKT) or GeoJSON. If a resource has multiple spatial geometry properties, it is the decision of the server whether only a single spatial geometry property is used to determine the extent or all relevant geometries.

### Parameter geometryCrs

Asserts the CRS used for the coordinate values of the `geometry` parameter. The default is WGS 84 or WGS84h depending on whether ellipsoidal height is included or not:

- WGS 84 longitude/latitude ([`https://www.opengis.net/def/crs/OGC/1.3/CRS84`](https://www.opengis.net/def/crs/OGC/1.3/CRS84))
- WGS 84h longitude/latitude/ellipsoidal height ([`https://www.opengis.net/def/crs/OGC/0/CRS84h`](https://www.opengis.net/def/crs/OGC/0/CRS84h))

### Parameter limit

The optional limit parameter limits the number of items that are presented in the response document. Only items are counted that are on the first level of the collection in the response document. Nested objects contained within the explicitly requested items shall not be counted.

### Parameter ids

The optional `ids` parameter allows a specific list of resources, indicated by their identifiers, to be fetched from an OGC API accessible collection. Only resources whose identifier matches one of the values listed for this parameter shall appear in the result set.

### Parameter q

The optional `q` parameter supports keyword searching. Only resources whose text fields contain one or more of the specified search terms are selected. The specific set of text keys/fields/properties of a resource to which the `q` operator is applied is up to the discretion of the server. Implementations should, however, apply the `q` operator to the title, description and keywords keys/fields/properties if they exist in the resource.

### Parameter assets

The optional `assets` parameter indicates which assets to select from a list of potential candidates found within the Collection. While not necessarily limited to STAC, it is a common example for illustrative purpose. The `assets` would indicate the STAC Assets to select by name from a STAC Collection where Items offer multiple Assets. The Assets can be resolved at the Collection level (i.e., `item_assets` or `assets`) or from individual Items. This selection is to be distinguished from [property selection](#sec-8.1.3.3) where the fields of those filtered `assets` are selected instead. The `assets` field might not apply to certain collection formats dealing directly with the data properties.

### Parameter crs

If the parameter is specified, then the coordinates of all geometry-valued properties in a response document are in the requested CRS. Otherwise the coordinates are in the default CRS, that is [`https://www.opengis.net/def/crs/OGC/1.3/CRS84`](https://www.opengis.net/def/crs/OGC/1.3/CRS84) for coordinates without height and [`https://www.opengis.net/def/crs/OGC/0/CRS84h`](https://www.opengis.net/def/crs/OGC/0/CRS84h) for coordinates with ellipsoidal height.

## Property selection & derived properties

<!-- requirement: collection-input/property-selection -->

### Parameter properties

A filter that selects resource properties to be included in a response document. The elements in the `properties` parameter can be the names of resource properties, aliases for resources properties or synthetic properties. Synthetic properties are properties that are computed on the fly and can reference resource property names or aliases for resource properties.

### Parameter aliases

A dictionary of `aliases` that can be used as values for the `properties` parameter. Aliases can be alternative names for resource properties or synthetic properties. Synthetic properties are named expressions that are computed at run-time. Expressions for synthetic properties are encoded using some expression language and can include references to resource property names or aliases for resource properties.

## Pass through parameters

<!-- requirement: collection-input/pass-through -->

The `passThroughParameters` property is a dictionary of query parameters that are passed directly to the value source server. The keys used in this object should be identical to query parameters that the value source server recognizes.

In the case where the OAProc server supports local filtering, the `passThroughParameters` property provides a mechanism to force filtering to occur on the value source server.

# Examples

**Example — An example execute request with collection input**

```json
{
  "$comment": "This example executes a process called `isotermal`. This process accepts a collection of features that include a position and a temperature and this process uses that information to generate an isothermal map.",
  "inputs": {
    "features": {
       "collection": "/collection/temps",
       "aliases": {
          "geometry": "pos",
          "acquisition-date": "acq",
          "tempK": {
            "expressionLang": "cql2-text",
            "expression": "tempC+273.15"
          },
          "tempF": {
            "expressionLang": "cql2-json",
            "expression": {
              "op": "+",
              "args": [
                { 
                  "op": "*",
                  "args": [ { "property": "tempC" }, 1.8 ]
                },
                32
              ]
            }
          }
       },
       "properties": [
         "pos",
         "acq",
         "tempC",
         "tempF",
         "tempK"
       ],
       "datetime": "2025-01-01T00:00:00/..",
       "geometry": "POLYGON((-79.639212 43.712105, -79.192306 43.855457, -79.121321 43.782197, -79.521818 43.585996, -79.639212 43.712105))"
    }
  },
  "outputs": {
    "isothermalmap": { }
  }
}
```

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/requirements/collectionInput`

