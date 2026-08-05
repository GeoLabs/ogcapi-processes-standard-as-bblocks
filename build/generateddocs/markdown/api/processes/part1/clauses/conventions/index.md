
# Conventions (Clause)

`ogc.api.processes.part1.clauses.conventions` *v2.0.0*

Conventions used throughout OGC API — Processes Part 1: Core.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This section provides details and examples for conventions used in the document.

## Identifiers

The normative provisions in this Standard are denoted by the URI:

```
http://www.opengis.net/spec/ogcapi-processes-1/2.0
```

All requirements, permissions, recommendations, and conformance tests that appear in this document
are denoted by partial URIs which are relative to this base.

## APIs

This Standard is primarily concerned with defining the components of a Processes API — an API that
enables the execution of computing processes, the retrieval of metadata describing their purpose and
functionality, and the retrieval of the results of the process execution. Implementations of the
Processes API may be embedded as part of a broader API (for example, a single server implementing
both OGC API — Features and OGC API — Processes). When the term "API" is encountered in this
Standard, it refers only to the Processes API components.

## Schemas

Schemas defined in this Standard use the [JSON Schema](https://json-schema.org/specification)
standard and are encoded in [YAML](https://yaml.org/spec/1.2.2/).

## Link relations

To express relationships between resources, [RFC 8288 (Web Linking)](https://www.rfc-editor.org/rfc/rfc8288)
is used. The following link relation types are used:

| Relation | Description |
|---|---|
| `service` | Indicates a URI that can be used to retrieve a service document. |
| `alternate` | Refers to a substitute for the link's context. |
| `service-desc` | Identifies a service description primarily intended for machines (e.g. an OpenAPI definition). |
| `service-doc` | Identifies service documentation primarily intended for humans. |
| `self` | Conveys an identifier for the link's context. |
| `up` | Refers to a parent document in a hierarchy. |
| `profile` | Refers to a profile of a resource. |
| `http://www.opengis.net/def/rel/ogc/1.0/conformance` | Refers to a resource that identifies the specifications that the link's context conforms to. |
| `http://www.opengis.net/def/rel/ogc/1.0/processes` | Points to the list of processes the API offers. |
| `http://www.opengis.net/def/rel/ogc/1.0/execute` | Points to the execution endpoint of the server. |
| `http://www.opengis.net/def/rel/ogc/1.0/job-list` | Points to the list of jobs. |
| `http://www.opengis.net/def/rel/ogc/1.0/results` | Points to the results of a job. |

## Use of HTTPS

For simplicity, this Standard only refers to the HTTP protocol. This is not meant to exclude the
use of HTTPS. In fact, most servers are expected to use HTTPS. OGC Web API Standards do not
prohibit the use of any valid HTTP option.

## HTTP URIs

This Standard does not restrict the lexical space of URIs beyond the requirements of the HTTP and
URI Syntax IETF RFCs. Reserved characters that are delimiters in URI subcomponents must be
percent-encoded. See Clause 2 of [RFC 3986](https://www.rfc-editor.org/rfc/rfc3986) for details.


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/clauses/conventions`

