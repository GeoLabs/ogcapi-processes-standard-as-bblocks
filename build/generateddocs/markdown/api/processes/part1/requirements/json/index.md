
# JSON (Requirements-class)

`ogc.api.processes.part1.requirements.json` *v2.0.0*

Requirements class for JSON encoding. Requires that all supported API endpoints respond with application/json when requested.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This requirements class specifies the JSON encoding for OGC API — Processes responses.

The JSON encoding is one of two pre-defined encodings (the other being HTML). It applies to all
standard API responses: the landing page, conformance declaration, process list, process
description, and job status endpoints. The encoding of process output values is independent of this
requirement — output values can be of any type regardless of whether the server supports the JSON
requirements class.

Servers supporting multiple encodings must provide encoding-specific URIs for resources (for
example, via format-specific path suffixes like `.json` or a query parameter such as `f=json`) so
that links to alternate representations can be expressed.

<!-- requirements -->

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/is/18-062r2/18-062r2.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/json`

