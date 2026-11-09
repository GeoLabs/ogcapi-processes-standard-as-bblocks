
# Requirements classes for encodings (Clause)

`ogc.api.processes.part1.clauses.encodings` *v2.0*

Encodings clause of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3), grouping the JSON and HTML requirements classes.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

This clause specifies two pre-defined requirements classes for request and response message encodings to be used by implementations of the Processes API. The two classes are:

- [JSON](#sec-10.2)
- [HTML](#sec-10.3)

The [JSON](#sec-10.2) requirements class defines the requirements for encoding Processes API request and response messages using [JSON](https://tools.ietf.org/html/rfc8259).

The [HTML](#sec-10.2) requirements class defines the requirements for encoding Processes API request and response messages using [HTML](https://html.spec.whatwg.org/).

**NOTE 1:** The encoding of Processes API request and response messages is distinct from the values that are generated when executing a process. Process output values can be of any type and are not bound by the requirements of the classes defined in this clause.

**NOTE 2:** Any server that supports multiple response encodings (JSON or HTML defined in this Standard or other encodings not specified in this Standard) will have to support a mechanism to mint encoding-specific URIs for resources to express links, for example, to alternate representations of the same resource. This document does not mandate any approach as to how this is supported by the server.

As clients simply need to dereference the URI of the link, the implementation detail and the mechanism as to how the encoding is included in the URI of the link are not important. Developers interested in the approach of a particular implementation, for example, to manipulate (“hack”) URIs in the browser address bar, can study the API definition.

Two common approaches are:

- An additional path for each encoding of each resource (this can be expressed, for example, using format specific suffixes like `.html`);
- An additional query parameter (for example, “accept” or “f”) that overrides the Accept header of the HTTP request.

The [Core](#bb-ogc-api-processes-part1-requirements-core) requirements class includes recommendations to support [HTML](#bb-ogc-api-processes-part1-requirements-html) and [JSON](#bb-ogc-api-processes-part1-requirements-json) as encodings, where practical.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/clauses/encodings`

