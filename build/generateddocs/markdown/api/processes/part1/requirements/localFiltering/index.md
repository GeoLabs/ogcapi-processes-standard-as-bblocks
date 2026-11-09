
# Local Filtering (Requirements-class)

`ogc.api.processes.part1.requirements.localFiltering` *v2.0*

Requirements class “Local Filtering” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): filtering of input values by the processing server.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

As described in [Clause 8.1.3.2](#sec-8.1.3.2), implementation of this Standard that support [collection input](#sec-8.1) rely on the [value source server](#sec-4.1.22) to perform any input data filtering specified in an execution request.

Servers that implement this Requirements Class, support local filtering in those instances where the [value source server](#sec-4.1.22) does not support the input data filtering requested in the execution request.

<!-- requirements-class -->

# Filter parameters

<!-- requirement: local-filtering -->

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/localFiltering`

