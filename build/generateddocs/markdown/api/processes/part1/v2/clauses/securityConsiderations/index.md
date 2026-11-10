
# Security Considerations (Clause)

`ogc.api.processes.part1.v2.clauses.securityConsiderations` *v2.0*

Security considerations of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): HTTP GET operations, the execute operation and the dismiss operation.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The OGC API — Processes Standard makes use of different HTTP methods, namely GET, POST and DELETE. (Note that future extensions could introduce additional HTTP methods.)

HTTP methods can be classified as

- Safe, meaning that they do not alter the state of (a resource on) the server, and
- Idempotent, meaning that can be executed an indefinite number of times and deliver the same result.

[Table 1](#http_methods_safety) gives an overview of the classification of HTTP the methods used in this standard:

**Table 1 — Classification of HTTP methods**

<div id="http_methods_safety"></div>

<table>
<thead><tr><th>HTTP Method</th><th>Safe</th><th>Idempotent</th></tr></thead><tbody><tr><td>GET</td><td>yes</td><td>yes</td></tr><tr><td>POST</td><td>no</td><td>no</td></tr><tr><td>DELETE</td><td>no</td><td>yes</td></tr><tr><td colspan="3">Source <a href="#rfc7231">RFC 7231, Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content</a></td></tr></tbody>
</table>

The following resources can be retrieved using the safe HTTP GET operation and can contain sensitive information:

Requirements class “Core”:

- [Process list](#sec-7.10)
- [Process description](#sec-7.11)
- [Job status info](#sec-7.13)
- [Job results](#sec-7.14)

Requirements class “Job list”

- [list](#sec-12)

The following API — Processes operations use unsafe HTTP methods, modify resources and therefore require special attention:

Requirements class “Core”:

- [Execute](#sec-7.12), HTTP POST

Requirements class “Dismiss”

- [Dismiss](#sec-14), HTTP DELETE

# Operations using HTTP GET

Most of the operations defined in the OGC API — Processes Standard use the safe HTTP GET operation. However, the resources that are returned by these operations contain information that could be used to exploit implementations of the Processes API. [Table 2](#table_core_safe_operations_security) gives an overview of the resources specified in this standard and what kind of information they contain.

**Table 2 — Requirements class ‘Core’ — Overview of core operations and returned sensitive information**

<div id="table_core_safe_operations_security"></div>

| Resource | Path | HTTP method | Information delivered |
|---|---|---|---|
| Landing page | `/` | GET | General information about the service, links to API endpoints |
| Conformance classes | `/conformance` | GET | List of conformance classes |
| Process list | `/processes` | GET | Process identifiers, links to process descriptions |
| Process description | `/processes/{processID}` | GET | Information about a process, e.g. inputs/outputs |
| Job status info | `/jobs/{jobID}` | GET | Status info, links to results or exceptions |
| Job results | `/jobs/{jobID}/results` | GET | Job results |

The following is more detailed information on the resources:

- The landing page can include links to endpoints, that are not defined in the API — Processes Standard, which can link to all the other resources that the containing API might offer.
- The list of conformance classes could contain information about extensions such as “dismiss” that pose additional security issues.
- The process list contains process identifiers and links to the respective process descriptions.
- The process description contains all necessary information needed to execute a process. This information can be used to send a JSON [execute request](#execute-request-body) to the Processes API endpoint that will pass initial sanity checks. For example, checks for the correct input/output identifiers. The ability to pass values to the server is vulnerable to injection attacks and issues discussed in section [Clause IV.B](#sec-IV.B) can occur.
- The job status info contains not only status information, but for finished processes also links to results / exceptions. The results of a process execution are a valuable resource as well as the exceptions that could contain hints about why the execution has failed.

**Table 3 — Requirements class ‘Job List’ — Overview of operations and returned sensitive information**

| Resource | Path | HTTP method | Information delivered |
|---|---|---|---|
| Job list | `/jobs` | GET | List of job IDs and status info, links to results or exceptions |

The retrieval of the job list of a process returns the job IDs and links to the respective job status.

# Execute operation

The *execute* operation uses HTTP POST to create new processing jobs (process executions). As discussed above, the HTTP POST method is not safe and its use poses the following threats if misused:

- The processing can require considerable server resources including, for example, computing time, network traffic (when accessing referenced inputs) or storage space for inputs and outputs.
- Malicious inputs can be encoded either inline in the [execute request](#execute-request-body) JSON or by reference by providing URIs to malicious input values in the [execute request](#execute-request-body) JSON.

**Table 4 — Requirements class ‘Core’ — Overview of the execute operation and returned sensitive information**

| Resource | Path | HTTP method | Information delivered |
|---|---|---|---|
| Job status info | `/jobs` | POST | Job id, status info, (links to) results or exceptions |

The new job IDs that are returned in the status info document should be created in a non-guessable way, for example by using UUIDs. This will prevent random attempts to get job status information, results / exceptions or even cancel jobs / delete job artifacts.

<!-- recommendation: job-list/access-control-job-list -->

# Dismiss operation

The optional *dismiss* extension uses the HTTP DELETE method and can be used to

- Cancel a running job, and
- Remove artifacts of a finished job.

Both usages pose security related issues. The cancellation of a running job (if not done on purpose) is wasting the resources that the job used prior to being cancelled. The same issue applies to the unwanted removal of artifacts of a finished job. If the *dismiss* extension is implemented, access control for the operation should be considered. The *dismiss* operation is idempotent, as it is specified by this Standard to be called using a specific job identifier. The first *dismiss* request to that identifier will result in a HTTP 200 (OK) status code. Continued *dismiss* requests using the same identifier result in a HTTP 410 (Gone) error code, but nothing else is changed on the server. A successful *dismiss* request returns a status info document containing the job identifier and the status “dismissed”. This status info document has no further security implications.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/clauses/securityConsiderations`

