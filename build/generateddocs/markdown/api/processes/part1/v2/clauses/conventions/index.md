
# Conventions (Clause)

`ogc.api.processes.part1.v2.clauses.conventions` *v2.0.0*

Conventions used throughout OGC API — Processes Part 1: Core.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This section provides details and examples for any conventions used in the document. Examples of conventions are symbols, abbreviations, use of XML schema, or special notes regarding how to read the document.

# Identifiers

The normative provisions in this Standard are denoted by the URI

[https://www.opengis.net/spec/ogcapi-processes-1/1.0](https://www.opengis.net/spec/ogcapi-processes-1/1.0)

All requirements, permission, recommendations, and conformance tests that appear in this document are denoted by partial URIs which are relative to this base.

# APIs

This Standard is primarily concerned with defining the components of a Processes API. That is an API that when implemented enables the execution of computing processes, the retrieval of metadata describing their purpose and functionality and the retrieval of the results of the process execution. The reader, however, should be cognizant of the fact that an implementation of the Processes API as defined in this Standard may be embedded as part of a broader deployed API. For example, a single server may implement the [Features](https://docs.ogc.org/is/17-069r4/17-069r4.html#_references) and Processes APIs. In this case, common elements (such as the landing page) will contain components of both standards.

**NOTE:** When the term “API” is encountered in this Standard, the term is in most cases referring only to the components of a Processes API even though an implementation of the Processes API may be part of a broader API implementation.

# Schemas

Schemas defined in this Standard are defined using the [JSON Schema](https://json-schema.org/specification) standard and are encoded using [YAML](https://yaml.org/spec/1.2.2/) which is a human-friendly data serialization language.

# Link relations

To express relationships between resources, [RFC 8288 (Web Linking)](#rfc8288) is used.

The following [link relation types](https://www.iana.org/assignments/link-relations/link-relations.xhtml) are used in this document.

- **service**: Indicates a URI that can be used to retrieve a service document (e.g. a service landing page).

- **alternate**: Refers to a substitute for the link’s context.

- **monitor**: Identifies a resource that can use used to monitor changes in a resource.

- **service-desc**: Identifies service description for the context that is primarily intended for consumption by machines.

  - API definitions are considered service descriptions.
  - In this Standard, [OpenAPI 3.0](https://swagger.io/specification/v3/) is used to provide a formal, machine readable, definition of the service but other API definition representations can also be used.

- **service-doc**: Identifies service documentation for the context that is primarily intended for human consumption.

- **self**: Conveys an identifier for the link’s context.

- **up**: Refers to a parent document in a hierarchy of documents.

- **profile**: Refers to a profile of a resource.

In addition, the following link relation types are used for which no applicable registered link relation type could be identified.

- **[https://www.opengis.net/def/rel/ogc/1.0/conformance](https://www.opengis.net/def/rel/ogc/1.0/conformance)**: Refers to a resource that identifies the specifications that the link’s context conforms to.
- **[https://www.opengis.net/def/rel/ogc/1.0/exceptions](https://www.opengis.net/def/rel/ogc/1.0/exceptions)**: The target URI points to exceptions of a failed process.
- **[https://www.opengis.net/def/rel/ogc/1.0/execute](https://www.opengis.net/def/rel/ogc/1.0/execute)**: The target URI points to the execution endpoint of the server.
- **[https://www.opengis.net/def/rel/ogc/1.0/job-list](https://www.opengis.net/def/rel/ogc/1.0/job-list)**: The target URI points to the list of jobs.
- **[https://www.opengis.net/def/rel/ogc/1.0/processes](https://www.opengis.net/def/rel/ogc/1.0/processes)**: The target URI points to the list of processes the API offers.
- **[https://www.opengis.net/def/rel/ogc/1.0/results](https://www.opengis.net/def/rel/ogc/1.0/results)**: The target URI points to the results of a job.

Each resource representation includes an array of links. Implementations are free to add additional links for all resources provided by an implementation of the Processes API.

# Use of HTTPS

For simplicity, this Standard only refers to the HTTPS protocol. This is not meant to exclude the use of HTTP. This is simply a shorthand notation for “HTTP or HTTPS”. In fact, most servers are expected to use [HTTPS](#rfc2818), not [HTTP](#rfc2616).

OGC Web API Standards do not prohibit the use of any valid HTTP option. However, implementers should be aware that optional capabilities which are not in common use could be an impediment to interoperability.

# HTTP URIs

This Standard does not restrict the lexical space of URIs used in an implementation of the Processes API beyond the requirements of the [HTTP](#rfc2616) and [URI Syntax](#rfc3986) IETF RFCs. If URIs include reserved characters that are delimiters in the URI subcomponent, these must be percent-encoded. See Clause 2 of [RFC 3986 (URI Syntax)](#rfc3986) for details.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/clauses/conventions`

