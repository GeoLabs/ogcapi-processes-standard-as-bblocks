
# JSON (Requirements-class)

`ogc.api.processes.part1.v2.requirements.json` *v2.0.0*

Requirements class for JSON encoding. Requires that all supported API endpoints respond with application/json when requested.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This section defines the JSON Requirements Class.

<!-- requirements-class -->

<!-- requirement: json/definition -->

**NOTE:** Responses from the execution endpoint [`/processes/{processID}/execution`](#sec-7.12) may or may not generate JSON depending on the process being executed, the [negotiated execution mode](#sec-7.12.2.2), the negotiated response format (specified using the [HTTP Accept](https://www.rfc-editor.org/rfc/rfc2616#section-14.1) header or the [`f`](#req-kvp-execute-f-definition) query parameter) and the [number of requested outputs](#req-core-process-execute-sync-many-json).

<!-- permission: json/media-types -->

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/requirements/json`

