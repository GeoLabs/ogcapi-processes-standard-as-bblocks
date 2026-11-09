
# Scope (Clause)

`ogc.api.processes.part2.clauses.scope` *v1.0.0*

Scope clause for OGC API — Processes Part 2: Deploy, Replace, Undeploy (DRAFT).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The OGC API — Processes — Part 2 Standard is an extension to the OGC API – Processes – Part 1: Core Standard \[[OGC 18-062r2](#OAProc-1)\] and defines the behavior of a server that supports the ability to dynamically add, replace and/or undeploy processes via an OGC API — Processes implementation instance.

Specifically, the Processes Part 2 Standard specifies:

- How to deploy a new process.
- How to replace an existing process.
- How to undeploy an existing process.

The following table crosswalks each of the resource endpoints discussed in this Standard with the HTTP methods POST, PUT and DELETE. Each intersecting cell in the table either contains the name of the operation for that combination of resource endpoint and HTTP method, or it contains the phrase “n/a” which is used to indicate that this Standard does not specify any behavior for that combination of resource endpoints and the HTTP method.

**Table 1 — Supported HTTP methods by resource**

<table><colgroup><col><col><col><col><col></colgroup><thead><tr><th>Resource endpoint</th><th colspan="4">HTTP method</th></tr></thead><tbody><tr><td></td><td><b>GET</b></td><td><b>POST</b></td><td><b>PUT</b></td><td><b>DELETE</b></td></tr><tr><td><tt>/processes</tt></td><td>n/a</td><td><a href="#sec-6.6">deploy</a></td><td>n/a</td><td>n/a</td></tr><tr><td><tt>/processes/{processID}</tt></td><td>n/a</td><td>n/a</td><td><a href="#sec-6.7">replace</a></td><td><a href="#sec-6.8">undeploy</a></td></tr><tr><td><tt>/processes/{processID}/package</tt></td><td><a href="#sec-6.9">package</a></td><td>n/a</td><td>n/a</td><td>n/a</td></tr></tbody></table>

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/clauses/scope`

