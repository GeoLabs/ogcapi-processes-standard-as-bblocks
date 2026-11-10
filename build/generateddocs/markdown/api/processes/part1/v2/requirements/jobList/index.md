
# Job list (Requirements-class)

`ogc.api.processes.part1.v2.requirements.jobList` *v2.0*

Requirements class “Job list” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): list of jobs with optional filtering.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

The Job list Requirements Class specifies the requirements for a request that retrieves a list of jobs from a Processes API endpoint.

<!-- requirements-class -->

# Operation

## Job list

<!-- requirement: job-list/job-list-op -->

<!-- recommendation: job-list/job-list-landing-page -->

## Parameter type

<!-- requirement: job-list/type-definition -->

<!-- requirement: job-list/type-response -->

## Parameter processID

<!-- requirement: job-list/processID-mandatory -->

<!-- requirement: job-list/processID-definition -->

<!-- requirement: job-list/processid-response -->

## Parameter status

<!-- requirement: job-list/status-definition -->

<!-- requirement: job-list/status-response -->

## Parameter datetime

<!-- requirement: job-list/datetime-definition -->

<!-- requirement: job-list/datetime-response -->

## Parameter minDuration, maxDuration

<!-- requirement: job-list/duration-definition -->

<!-- requirement: job-list/duration-response -->

## Parameter limit

<!-- requirement: job-list/limit-definition -->

<!-- permission: job-list/limit-default-minimum-maximum -->

<!-- requirement: job-list/limit-response -->

<!-- permission: job-list/limit-response -->

# Response

<!-- requirement: job-list/job-list-success -->

```yaml
type: object
required:
  - jobs
  - links
properties:
  jobs:
    type: array
    items:
      $ref: "statusInfo.yaml"
  links:
    type: array
    items:
      $ref: "link.yaml"
```

**Listing 59 — Schema for the job list**

**NOTE:** This schema can also be obtained from [`jobList.yaml`](https://raw.githubusercontent.com/opengeospatial/ogcapi-processes/master/openapi/schemas/processes-core/jobList.yaml).

(see also: [statusInfo.yaml](#schema-statusInfo), [link.yaml](#link-schema))

The schema defines an array of [status info elements](#schema-statusInfo) and includes a links section for navigation links within the API.

The number of jobs returned depends on the server and the parameter `limit.`

See the discussion about the `limit` parameter in the [Limit parameter](#sec-7.8) section.

<!-- requirement: job-list/links -->

See the discussion about the `next` links in the [Limit parameter](#next-link-discussion) section.

<!-- recommendation: job-list/next-1 -->

<!-- recommendation: job-list/next-2 -->

<!-- recommendation: job-list/next-3 -->

See the discussion about the `prev` link in the [Limit parameter](#prev-link-discussion) section.

<!-- permission: job-list/prev -->

**Example 1 — A HTTP GET request for retrieving a list of jobs encoded as JSON.**

```
https://processing.example.org/jobs
```

**Example 2 — A job list encoded as JSON.**

```json
{
  "jobs": [
    {
      "processID": "Voronoi",
      "jobID": "8ca109b4-3b86-4a9c-a284-a6d50f91019e",
      "status": "running",
      "message": "Perform step 1/2",
      "progress": 50,
      "links": [
        {
          "href": "http://processing.example.org/oapi-p/jobs/8ca109b4-3b86-4a9c-a284-a6d50f91019e",
          "rel": "status",
          "type": "application/json",
          "hreflang": "en",
          "title": "Job status"
        }
      ]
    },
    {
      "processID": "EchoProcess",
      "jobID": "0cf773a5-282a-4e23-96cc-f5dab18123e5",
      "status": "successful",
      "message": "EchoProcess job finished successful",
      "progress": 100,
      "links": [
        {
          "href": "http://processing.example.org/oapi-p/jobs/0cf773a5-282a-4e23-96cc-f5dab18123e5",
          "rel": "status",
          "type": "application/json",
          "hreflang": "en",
          "title": "Job status"
        },
        {
          "href": "http://processing.example.org/oapi-p/jobs/0cf773a5-282a-4e23-96cc-f5dab18123e5/results",
          "rel": "http://www.opengis.net/def/rel/ogc/1.0/results",
          "type": "application/json",
          "hreflang": "en",
          "title": "Job result"
        }
      ]
    },
    {
      "processID": "EchoProcess",
      "jobID": "63aadd9c-c0e5-4a7f-80f0-228dbb158f09",
      "status": "failed",
      "message": "EchoProcess job failed",
      "progress": 100,
      "links": [
        {
          "href": "http://processing.example.org/oapi-p/jobs/63aadd9c-c0e5-4a7f-80f0-228dbb158f09",
          "rel": "status",
          "type": "application/json",
          "hreflang": "en",
          "title": "Job status"
        },
        {
          "href": "http://processing.example.org/oapi-p/jobs/63aadd9c-c0e5-4a7f-80f0-228dbb158f09/results",
          "rel": "http://www.opengis.net/def/rel/ogc/1.0/exceptions",
          "type": "application/json",
          "hreflang": "en",
          "title": "Job exception"
        }
      ]
    }
  ],
  "links": [
    {
      "href": "http://processing.example.org/jobs?limit3&f=json",
      "rel": "self",
      "type": "application/json"
    },
    {
      "href": "http://processing.example.org/jobs?f=html",
      "rel": "alternate",
      "type": "text/html"
    },
    {
       "href": "http//processing.example.org/jobs?offset=4&limit=3&f=json",
       "rel": "next"
    }
       
  ]
}
```

# Error situations

See [Clause 7.5.1](#sec-7.5.1) for general guidance.

If the process with the specified identifier does not exist on the server, the status code of the response SHALL be `404` (see [Requirement 16: `/req/core/process-exception-no-such-process`](#req-core-process-exception-no-such-process)).

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/requirements/jobList`

