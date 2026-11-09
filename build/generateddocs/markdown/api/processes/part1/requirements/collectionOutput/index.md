
# Collection Output (Requirements-class)

`ogc.api.processes.part1.requirements.collectionOutput` *v2.0*

Requirements class “Collection Output” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): process execution triggered through OGC API data access mechanisms.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

The *Collection Output* Requirements Class specifies how the execution of a process can be triggered as the result of requesting output data using an [OGC API data access mechanisms](#sec-4.1.10).

This provides an alternative to the synchronous and asynchronous execution mechanisms defined in this Standard for which spatial, temporal and other filtering parameters would need to be hardcoded in the [execute request](#execute-request-body). When lengthy batch processing is not desirable, completely new [execute requests](#execute-request-body) each with different spatial, temporal and other filtering parameters and returning a partial output would need to be continuously re-submitted.

This conformance class supports submitting an [execute request](#execute-request-body) once and then accessing the output using [OGC API data access mechanisms](#sec-4.1.10) in a manner that is completely agnostic of process execution.

Compared to separate [execute requests](#execute-request-body), this mechanism makes it easier for implementations to optimize for scenarios where small partial outputs are streamed from the same pre-established processing pipeline. Parsing the [execute request](#execute-request-body), validating inputs, and handshakes with remote components only needs to be performed once. An implementation could also preempt future requests based on past requests, offsetting the latency of a complex processing pipeline.

<!-- requirements-class -->

The following requirements describe an execution mechanism that triggers on-demand processing for particular spatial, temporal and other filtering parameters and results in one or more references to a [collection description document](#sec-4.1.2) that provides links to request output data using standard [OGC API data access mechanisms](#sec-4.1.10).

# Parameter response

<!-- requirement: collection-output/response-definition -->

<!-- permission: collection-output/response-query -->

<!-- requirement: collection-output/response-output-one -->

<!-- permission: collection-output/response-output-one -->

<!-- requirement: collection-output/response-output-many-results -->

<!-- requirement: collection-output/response-output-many-grouped -->

**NOTE:** The [/req/collection-output/response-output-many-grouped](#req-collection-output-response-output-many-grouped) part mentioning aggregation is left up to server implementations to negotiate and resolve as deemed fit. For example, a process generating multiple GeoTiff rasters as separate bands per output and requesting the collection output could either aggregate each band as separate Assets under a *STAC Collection* and/or *STAC Items*, or could generate an *OGC API — Coverages* collection by combining bands over corresponding extents. The specific separation of STAC Collection/Items/Assets, Coverage granules, or any other aggregation strategy is out of scope for this standard. However, [Clause 7.7](#sec-7.7) would realistically play a role in this process to further distinguish possible combinations and expected outcomes.

# Error Situations

<!-- requirement: collection-output/response-unsupported -->

# Data Access Mechanisms

<!-- requirement: collection-output/data-access-mechanisms -->

This Standard does not impose any particular approach to materializing output [collections](#sec-4.1.1) resulting from a process execution request.

<!-- permission: collection-output/static -->

<!-- permission: collection-output/dynamic -->

# Collection Output expiry

<!-- permission: collection-output/expiry -->

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/collectionOutput`

