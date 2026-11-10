
# HTML (Requirements-class)

`ogc.api.processes.part1.v2.requirements.html` *v2.0*

Requirements class “HTML” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): HTML encoding of the API responses.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This section defines the HTML Requirements Class.

<!-- requirements-class -->

<!-- requirement: html/definition -->

**NOTE:** Responses from the execution endpoint [`/processes/{processID}/execution`](#sec-7.12) may or may not generate HTML depending on the process being executed, the [negotiated execution mode](#sec-7.12.2.2), the negotiated response format (specified using the [HTTP Accept](https://www.rfc-editor.org/rfc/rfc2616#section-14.1) header or the [`f`](#req-kvp-execute-f-definition) query parameter) and the [number of requested outputs](#req-core-process-execute-sync-many-json).

<!-- permission: html/media-types -->

<!-- requirement: html/content -->

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/requirements/html`

