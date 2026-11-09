
# Callback (Requirements-class)

`ogc.api.processes.part1.requirements.callback` *v2.0*

Requirements class “Callback” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3): notification of completed jobs.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The Callback Requirements Class specifies a callback mechanism for completed jobs. In contrast to the pull-based mechanism specified in [Clause 7.12](#sec-7.12) and [Clause 7.13](#sec-7.13), this requirements class specifies a push-based mechanism, where a subscriber-URL is passed to the Processes API endpoint in the [execute request](#execute-request-body). After the job is completed, the result response is sent to the specified URL.

<!-- requirements-class -->

<!-- requirement: callback/job-callback -->

**Example — A callback in the execute operation**

```yaml
callbacks:
    jobCompleted:
      '{$request.body#/subscriber/successUri}':
        post:
          requestBody:
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/results'
          responses:
            '202':
              description: Results received successfully
```

Adding multiple callbacks is possible for getting progress updates and notifications of the success or failure of a job completion.

Further guidance about how to use callbacks can be found in the [OpenAPI documentation](https://swagger.io/docs/specification/callbacks/).

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/callback`

