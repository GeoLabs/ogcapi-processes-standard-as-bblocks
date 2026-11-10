# Introduction

OGC Web Application Programming Interfaces (APIs) are not Web Services in the traditional sense. Rather, they define the behavior and content of a set of Resources exposed through a Web API. Therefore, an API endpoint may expose resources in addition to those defined by the standard. A test engine must be able to traverse an implementation of the API, identify and validate test points, and ignore resource paths which are not to be tested.

The Web API under test can require authorization. Any Executable Test Suite implementing this test suite should implement the following security schemes supported by OpenAPI 3.0: HTTP Authorization schemes “basic” and “bearer”, API keys, and OAuth2 flow “authorizationCode”.

The following requirements apply for a server implementing the OGC API — Processes — Part 2: Deploy, Replace, Undeploy under test:

<!-- abstract-test: dru/mutable-process -->

In case both an [OGC Application Package](bblocks://ogc.api.processes.part2.v1.requirements.ogcapppkg) and [CWL](bblocks://ogc.api.processes.part2.v1.requirements.cwl) conformance classes are supported, the following requirement applies for a server implementing the OGC API — Processes — Part 2: Deploy, Replace, Undeploy being tested:

<!-- abstract-test: dru/test-process -->

# Conformance Class Deploy, Replace, Undeploy

<!-- conformance-class: ogc.api.processes.part2.v1.requirements.dru -->

## Immutable processes

<!-- abstract-test: dru/static-indicator -->

## Deploy operation

<!-- abstract-test: dru/deploy-post-op -->

<!-- abstract-test: dru/deploy-content-type -->

<!-- abstract-test: dru/deploy-unsupported-media-type -->

## Replace operation

<!-- abstract-test: dru/replace-put-op -->

<!-- abstract-test: dru/replace-content-type -->

## Undeploy operation

<!-- abstract-test: dru/undeploy-delete-op -->

<!-- abstract-test: dru/undeploy-response -->

<!-- abstract-test: dru/undeploy-response-immutable -->

# Conformance Class OGC Application Package

<!-- conformance-class: ogc.api.processes.part2.v1.requirements.ogcapppkg -->

## Deploy operation

<!-- abstract-test: ogcapppkg/deploy-body -->

<!-- abstract-test: ogcapppkg/deploy-response -->

<!-- abstract-test: ogcapppkg/deploy-response-success -->

<!-- abstract-test: ogcapppkg/deploy-response-duplicate -->

## Replace operation

<!-- abstract-test: ogcapppkg/replace-body -->

<!-- abstract-test: ogcapppkg/replace-response -->

# Conformance Class Docker

<!-- conformance-class: ogc.api.processes.part2.v1.requirements.docker -->

## Deploy operation

<!-- abstract-test: docker/deploy-body -->

## Replace operation

<!-- abstract-test: docker/replace-body -->

# Conformance Class CWL

<!-- conformance-class: ogc.api.processes.part2.v1.requirements.cwl -->

## Deploy operation

<!-- abstract-test: cwl/deploy-body -->

## Replace operation

<!-- abstract-test: cwl/replace-body -->
