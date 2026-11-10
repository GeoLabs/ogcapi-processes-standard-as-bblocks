
# Dismiss (Requirements-class)

`ogc.api.processes.part1.v2.requirements.dismiss` *v2.0*

Requirements class “Dismiss” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): cancelling active jobs or deleting completed jobs.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The Dismiss requirement class specifies how to dismiss a job.

When a job is dismissed, the operation can include the cancellation of a pending or running job, the removal of artifacts from a running or finished job, a combination of both, and further data management procedures not specifically prescribed by this standard.

<!-- requirements-class -->

# Operation

<!-- requirement: dismiss/job-dismiss-op -->

<!-- requirement: dismiss/job-dismiss-status -->

**NOTE:** This standard makes no statements regarding the disposition strategy of artifacts created by a job once a job has been dismissed and is no longer accessible via the Processes API. Responses to dismissed jobs and their artifacts can optionally employ the corresponding [/per/core/job-results-exception-job-gone](#per-core-job-results-exception-job-gone) and [/per/core/process-exception-job-gone](#per-core-process-exception-job-gone) approaches to indicate their unavailability.

# Response

<!-- requirement: dismiss/job-dismiss-success -->

**Example — A dismissed job encoded as JSON.**

```json
{
  "jobID" : "81574318-1eb1-4d7c-af61-4b3fbcf33c4f",
  "status": "dismissed",
  "message": "Job dismissed",
  "progress": 56,
  "links": [
    {
      "href": "http://processing.example.org/oapi-p/jobs",
      "rel": "up",
      "type": "application/json",
      "title": "The job list of this server"
    }
  ]
}
```

# Error situations

See [Clause 7.5.1](#sec-7.5.1) for general guidance.

If the process with the specified identifier does not exist on the server, the status code of the response SHALL be `404` (see [/req/core/process-exception/no-such-process](#req-core-process-exception-no-such-process)).

If the job with the specified identifier does not exist, the status code of the response SHALL be `404` (see [/req/core/job-results-exception/no-such-job](#req-core-job-exception-no-such-job)).

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/v2/requirements/dismiss`

