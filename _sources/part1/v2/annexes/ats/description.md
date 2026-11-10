# Introduction

OGC Web Application Programming Interfaces (APIs) are not Web Services in the traditional sense. Rather, they define the behavior and content of a set of Resources exposed through a Web API implementation instance. Therefore, an API endpoint may expose resources in addition to those defined by the standard. A test engine must be able to traverse the API definition, identify and validate test points, and ignore resource paths which are not to be tested.

The following requirement applies for a server implementing the OGC API — Processes — Part 1: Core under test:

<!-- requirement: core/test-process -->

<!-- recommendation: core/test-process -->

# Conformance Class Core

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.core -->

# Testable process

<!-- abstract-test: core -->

# Retrieve the API landing page

<!-- abstract-test: core/landingpage-op -->

<!-- abstract-test: core/landingpage-success -->

**NOTE:** The landing page may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the landing page against that schema. All supported formats should be exercised.

**Table A.1 — Schema and Tests for Landing Pages**

<div id="landing-page-schemas"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [landingPage.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/landingPage.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [landingPage.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/landingPage.yaml) | [/conf/json/content](#ats-json-definition) |

# Retrieve an API definition

<!-- abstract-test: core/api-definition-op -->

<!-- abstract-test: core/api-definition-success -->

# Declaration of conformance classes

<!-- abstract-test: core/conformance-op -->

<!-- abstract-test: core/conformance-success -->

# Use of HTTP 1.1

<!-- abstract-test: core/http -->

# Retrieve a process list

<!-- abstract-test: core/process-list-op -->

<!-- abstract-test: core/process-list-limit-definition -->

**NOTE 1:** An implementation of the Processes API can define different values for “minimum”, “maximum” and “default”.

<!-- abstract-test: core/process-list-limit-response -->

<!-- abstract-test: core/process-list-success -->

**NOTE 2:** The process list may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the against that schema. All supported formats should be exercised.

**Table A.2 — Schema and Tests for Lists content**

<div id="process-list-schema"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [processList.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/processList.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [processList.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/processList.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: core/process-list-links -->

<!-- abstract-test: core/process-summary-links -->

# Retrieve a process description

<!-- abstract-test: core/process-description-op -->

<!-- abstract-test: core/process-description-success -->

**NOTE:** The interface of a process may be described using one of a number of different models or process description languages. The following table identifies the applicable schema document for each process description model described in this standard.

**Table A.3 — Schema and Tests for Process Description Models**

| Model | Schema Document | Test ID |
|---|---|---|
| OGC Process Description JSON | [process.yaml](https://schemas.opengis.net/ogcapi/features/part1/2.0/openapi/schemas/process.yaml) | [/conf/ogc-process-description/json-encoding](#req-ogc-process-description-json-encoding) |

# Process exception

<!-- abstract-test: core/process-exception-no-such-process -->

**NOTE:** An exception response caused by using an invalid process identifier may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the response. All supported formats should be exercised.

**Table A.4 — Schema and Tests for Non-existent Process**

<div id="no-such-process"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

# Process execution /processes/{processID}/execution

<!-- abstract-test: core/process-execute-op -->

<!-- abstract-test: core/process-execute-request -->

<!-- abstract-test: core/process-execute-default-execution-mode -->

<!-- abstract-test: core/process-execute-auto-execution-mode -->

<!-- abstract-test: core/process-execute-input-array -->

<!-- abstract-test: core/process-execute-input-inline-object -->

<!-- abstract-test: core/process-execute-input-inline-multiple-types -->

<!-- abstract-test: core/process-execute-input-inline-binary -->

<!-- abstract-test: core/process-execute-input-inline-bbox -->

<!-- abstract-test: core/process-execute-input-validation -->

<!-- abstract-test: core/process-execute-omitted-outputs -->

<!-- abstract-test: core/process-execute-empty-outputs -->

<!-- abstract-test: core/process-execute-sync-one -->

<!-- abstract-test: core/process-execute-sync-one-default-content -->

<!-- abstract-test: core/process-execute-sync-many-json -->

<!-- abstract-test: core/process-execute-success-sync-outputs-omitted -->

<!-- abstract-test: core/process-execute-success-sync-empty-outputs -->

<!-- abstract-test: core/job-results-success-sync -->

<!-- abstract-test: core/process-execute-success-async -->

<!-- abstract-test: core/process-execute-success-async-outputs -->

<!-- abstract-test: core/process-execute-success-async-outputs-empty -->

<!-- abstract-test: core/process-execute-success-async-outputs-omitted -->

# Jobs

## Job status /jobs/{jobID}

<!-- abstract-test: core/job-op -->

<!-- abstract-test: core/job-success -->

**NOTE 1:** The status info page for a job may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the status info against that schema. All supported formats should be exercised.

**Table A.5 — Schema and Tests for the Job Status Info**

<div id="job-status-info-schema"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [statusInfo.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/statusInfo.yaml) | [/conf/html/content](#conf-html) |
| JSON | [statusInfo.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/statusInfo.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: core/job-exception-no-such-job -->

**NOTE 2:** An exception response caused by using an invalid job identifier may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the response. All supported formats should be exercised.

**Table A.6 — Schema and Tests for the Job Result for Non-existent Job**

<div id="job-exception-no-such-job"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

## Retrieve job results

<!-- abstract-test: core/job-results-op -->

<!-- abstract-test: core/job-results-param-outputs -->

**NOTE 1:** The API can define different values for “minimum”, “maximum” and “default”.

<!-- abstract-test: core/job-results-param-outputs-response -->

<!-- abstract-test: core/job-results-profile -->

<!-- abstract-test: core/job-result-op -->

<!-- abstract-test: core/job-results-async-one -->

<!-- abstract-test: core/job-results-async-many -->

<!-- abstract-test: core/job-results-exception-invalid-query-parameter-value -->

<!-- abstract-test: core/job-results-exception-no-such-output -->

**NOTE 2:** The job results page for a job may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the job results for a non-existent job against that schema. All supported formats should be exercised.

**Table A.7 — Schema and Tests for the Job Result for Non-existent Output**

<div id="job-results-exception-no-such-output"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](http://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](http://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: core/job-results-exception-no-such-job -->

**NOTE 3:** The job results page for a job may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the job results for a non-existent job against that schema. All supported formats should be exercised.

**Table A.8 — Schema and Tests for the Job Result for Non-existent Job**

<div id="job-results-exception-no-such-job"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: core/job-results-exception-results-not-ready -->

**NOTE 4:** The job results page for a job may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the job results for an incomplete job against that schema. All supported formats should be exercised.

**Table A.9 — Schema and Tests for the Job Result for an Incomplete Job**

<div id="job-results-exception-results-not-ready"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: core/job-results-exception_results-not-available -->

<!-- abstract-test: core/job-results-failed -->

**NOTE 5:** The job results page for a job may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the job results for a failed job against that schema. All supported formats should be exercised.

**Table A.10 — Schema and Tests for the Job Result for a Failed Job**

<div id="job-results-failed-schema"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [exception.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/exception.yaml) | [/conf/json/content](#ats-json-definition) |

# Collections

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.collectionInput -->

<!-- abstract-test: collection-input/referencing -->

<!-- abstract-test: collection-input/collection-access -->

<!-- abstract-test: collection-input/filtering -->

<!-- abstract-test: collection-input/property-selection -->

<!-- abstract-test: collection-input/pass-through -->

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.collectionOutput -->

<!-- abstract-test: collection-output/response-definition -->

<!-- abstract-test: collection-output/response-output-many-grouped -->

<!-- abstract-test: collection-output/response-output-many-results -->

<!-- abstract-test: collection-output/response-output-one -->

<!-- abstract-test: collection-output/response-unsupported -->

<!-- abstract-test: collection-output/data-access-mechanisms -->

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.remoteCollections -->

<!-- abstract-test: remote-collections/access -->

<!-- abstract-test: remote-collections/referencing -->

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.localFiltering -->

<!-- abstract-test: collection-input/local-filtering -->

# Conformance Class OGC Process Description

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.ogcProcessDescription -->

<!-- abstract-test: ogc-process-description/json-encoding -->

<!-- abstract-test: ogc-process-description/links -->

<!-- abstract-test: ogc-process-description/inputs-def -->

<!-- abstract-test: ogc-process-description/input-def -->

<!-- abstract-test: ogc-process-description/input-multiple-types -->

<!-- abstract-test: ogc-process-description/data-access-apis -->

<!-- abstract-test: ogc-process-description/outputs-def -->

<!-- abstract-test: ogc-process-description/output-def -->

<!-- abstract-test: ogc-process-description/output-multiple-types -->

# Conformance Classes for Encodings

## Conformance Class JSON

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.json -->

<!-- abstract-test: json/definition -->

## Conformance Class HTML

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.html -->

<!-- abstract-test: html/content -->

<!-- abstract-test: html/definition -->

# OpenAPI Conformance Classes

## Conformance Class OpenAPI Specification

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.oas -->

**Example 1**

**identifier**

/conf/oas/completeness

**target**

/req/oas/completeness

**test-purpose**

Verify the completeness of an OpenAPI document.

**test-method**

Verify that for each operation, the OpenAPI document describes all HTTP Status Codes and Response Objects that the API uses in responses.

**Example 2**

**identifier**

/conf/oas/exceptions-code

**target**

/req/oas/exceptions-codes

**test-purpose**

Verify that the OpenAPI document fully describes potential exception codes.

**test-method**

Verify that for each operation, the OpenAPI document describes all HTTP Status Codes that can be generated.

**Example 3**

**identifier**

/conf/oas/definition

**target**

/req/oas/definition

**test-purpose**

Verify that JSON and HTML versions of the OpenAPI document are available.

**test-method**

1. Verify that an OpenAPI definition in JSON is available using the media type `application/vnd.oai.openapi+json;version=x.y` (were `x.y` is the version of the OpenAPI specification used) and link relation `service-desc`
2. Verify that an HTML version of the API definition is available using the media type `text/html` and link relation `service-doc`.

**Example 4**

**identifier**

/conf/oas/implementation

**target**

/req/oas/implementation

**test-purpose**

Verify that all capabilities specified in the OpenAPI definition are implemented by the API.

**test-method**

1. Construct a path from each URL template including all server URL options and all enumerated path parameters.
2. For each path defined in the OpenAPI document, validate that the path performs in accordance with the API definition and the API-Features standard.

**Example 5**

**identifier**

/conf/oas/security

**target**

/req/oas/security

**test-purpose**

Verify that any authentication protocols implemented by the API are documented in the OpenAPI document.

**test-method**

1. Identify all authentication protocols supported by the API.
2. Validate that each authentication protocol is described in the OpenAPI document by a Security Schema Object and its use is specified by a Security Requirement Object.

## Conformance Class OpenAPI 3.0

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.oas30 -->

<!-- abstract-test: oas30/oas-definition -->

## Conformance Class OpenAPI 3.1

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.oas31 -->

<!-- abstract-test: oas31/oas-definition -->

# Conformance Class Job list

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.jobList -->

<!-- abstract-test: job-list/job-list-op -->

<!-- abstract-test: job-list/type-definition -->

<!-- abstract-test: job-list/type-response -->

<!-- abstract-test: job-list/processID-mandatory -->

<!-- abstract-test: job-list/processID-definition -->

<!-- abstract-test: job-list/processID-response -->

<!-- abstract-test: job-list/status-definition -->

<!-- abstract-test: job-list/status-response -->

<!-- abstract-test: job-list/datetime-definition -->

<!-- abstract-test: job-list/datetime-response -->

<!-- abstract-test: job-list/duration-definition -->

<!-- abstract-test: job-list/duration-response -->

<!-- abstract-test: job-list/limit-definition -->

**NOTE 1:** An implementation of the Processes API can define different values for “minimum”, “maximum” and “default”.

<!-- abstract-test: job-list/limit-response -->

<!-- abstract-test: job-list/links -->

**NOTE 2:** A job list may be retrieved in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate the against that schema. All supported formats should be exercised.

**Table A.11 — Schema and Tests for Job List Content**

<div id="job-list-schema"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [jobList.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/jobList.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [jobList.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/jobList.yaml) | [/conf/json/content](#ats-json-definition) |

<!-- abstract-test: job-list/job-list-success -->

# Conformance Class Callback

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.callback -->

<!-- abstract-test: callback/job-callback -->

# Conformance Class Dismiss

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.dismiss -->

<!-- abstract-test: dismiss/job-dismiss-op -->

<!-- abstract-test: dismiss/job-dismiss-success -->

**NOTE:** The response to dismissing a job can be presented in one of two formats. The following table identifies the applicable schema document for each format and the test to be used to validate against that schema. All supported formats should be exercised.

**Table A.12 — Schema and Tests for Dismissing a Job**

<div id="job-dismiss-schema"></div>

| Format | Schema Document | Test ID |
|---|---|---|
| HTML | [statusInfo.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/statusInfo.yaml) | [/conf/html/content](#ats-html-content) |
| JSON | [statusInfo.yaml](https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/statusInfo.yaml) | [/conf/json/content](#ats-json-definition) |

# Conformance Class KVP-encoded Execute

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.kvpExecute -->

<!-- abstract-test: kvp-execute/numeric-input-value -->

<!-- abstract-test: kvp-execute/string-input-value -->

<!-- abstract-test: kvp-execute/boolean-input-value -->

<!-- abstract-test: kvp-execute/complex-input-value -->

<!-- abstract-test: kvp-execute/array-input-value -->

<!-- abstract-test: kvp-execute/bbox-input-value -->

<!-- abstract-test: kvp-execute/bbox-crs-input-value -->

<!-- abstract-test: kvp-execute/binary-input-value -->

<!-- abstract-test: kvp-execute/binary-input-value-qualified -->

<!-- abstract-test: kvp-execute/input-by-reference -->

<!-- abstract-test: kvp-execute/input-cardinality -->

<!-- abstract-test: kvp-execute/input-query-parameters -->

<!-- abstract-test: kvp-execute/input-query-parameter-values -->

<!-- abstract-test: kvp-execute/process-execute-op -->

<!-- abstract-test: kvp-execute/output -->

<!-- abstract-test: kvp-execute/f-definition -->

<!-- abstract-test: kvp-execute/f-response -->

<!-- abstract-test: kvp-execute/prefer-definition -->

<!-- abstract-test: kvp-execute/prefer-response -->

# Conformance Class Profile query parameter

<!-- conformance-class: ogc.api.processes.part1.v2.requirements.queryParamProfile -->

<!-- abstract-test: query-param-profile/definition -->

<!-- abstract-test: query-param-profile/response -->
