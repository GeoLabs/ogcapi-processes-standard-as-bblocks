This Standard defines sixteen requirements / conformance classes.

The standardization targets of all conformance classes are “Web APIs.”

The main requirements class is:

- [Core](#bb-ogc-api-processes-part1-requirements-core).

The *Core* specifies requirements that any implementation of the Processes API in a Web API deployment must implement.

The *Core* does not mandate a specific encoding or format for the representation of resources defined in this Standard. Rather, two requirements classes depend on the *Core* and specify representations for the resources specified in the *Core* in commonly used encodings for data on the Web:

- [JSON](#bb-ogc-api-processes-part1-requirements-json), and
- [HTML](#bb-ogc-api-processes-part1-requirements-html).

Furthermore, the *Core* does not mandate any encoding or format for the formal definition of the Processes API. The OpenAPI specification is one option for defining the Processes API. As such, requirements classes have been specified for supporting OpenAPI and specifically OpenAPI 3.0 and 3.1, which depends on the requirements class *Core*:

- [OpenAPI Support](#bb-ogc-api-processes-part1-requirements-oas)
- [OpenAPI Specification 3.0](#bb-ogc-api-processes-part1-requirements-oas30)
- [OpenAPI Specification 3.1](#bb-ogc-api-processes-part1-requirements-oas31)

Implementors of the *Core* requirements class may also decide to use other API definition representations in addition to, or instead of, an OpenAPI 3.0 or 3.1 definition. Examples for alternative API definitions: OpenAPI 2.0 (Swagger), future versions of the OpenAPI specification, an OWS Common 2.0 capabilities document, or WSDL.

**NOTE:** OpenAPI offers an open, powerful and vendor neutral description format. While the use of OpenAPI for the formal definition of the API is not mandatory, the requests/responses of the API specified in this Standard are defined using OpenAPI 3.1 schemas. See also the note regarding [/req/core/landingpage-success](#req-core-landingpage-success)

An implementation of the *Core* is intended to be a minimally useful API for the execution of processes in the geospatial domain. The *Core* is designed to map the operations of a [Web Processing Service 2.0](https://docs.ogc.org/is/14-065/14-065r2.html) instance.

The *Core* does not mandate the use of any specific process description language to specify the interface of a process. Instead, this Standard defines and recommends the use of the following conformance class:

- [OGC Process Description](#bb-ogc-api-processes-part1-requirements-ogcprocessdescription)

This class defines an information model, encoded in JSON, which may be used to specify the interface of a process including the inputs that the process expects and the outputs that the process will generate.

Besides the standard input types one might expect for a process (e.g. integer, string, double, etc.) this Standard defines the following conformance class:

- [Collection Input](#bb-ogc-api-processes-part1-requirements-collectioninput)

that allows OGC API collections to be specified as process inputs. The [Collection Input](#bb-ogc-api-processes-part1-requirements-collectioninput) class only supports collections that are local to the current deployment to be specified as process inputs. The following conformance class:

- [Remote Collections](#bb-ogc-api-processes-part1-requirements-remotecollections)

extends the collection input requirements to support specifying remote collections as process inputs.

By default, the [Collection Input](#bb-ogc-api-processes-part1-requirements-collectioninput) and [Remote Collections](#bb-ogc-api-processes-part1-requirements-remotecollections) conformance classes rely on the data server being accessed for input values to provide filtering capabilities to identify the subset of data to be fed to a process as input values. The following conformance class:

- [Local Filtering](#bb-ogc-api-processes-part1-requirements-localfiltering)

defines requirements that allow the processing server itself to perform filtering of input values in the cases where the value source server does not support the requested filtering operations (e.g. applying a CQL2 filter to data from a server that does not support CQL2 filtering).

In addition to supporting collections as process inputs, the following conformance class:

- [Collection Output](#bb-ogc-api-processes-part1-requirements-collectionoutput)

defines requirements that allow process execution to be triggered by requesting output data using an standard [OGC API data access mechanisms](#sec-4.1.10). In this way, process execution becomes opaque, hidden behind a standard OGC data access API (e.g. features, coverages, etc.).

In the [Core](#bb-ogc-api-processes-part1-requirements-core) executing a process requires sending a JSON-encoded execution request to the server using the HTTP POST method. To support embedding process execution requests into other documents this Standard defines the:

- [KVP-encoded Execute](#bb-ogc-api-processes-part1-requirements-kvpexecute)

conformance class which allows process inputs to be encoded as query parameters on a URL and process execution to be invoked using the HTTP GET method.

The standard request and response encoding used in this Standard is JSON. The standard media type for JSON is `application/json` which does not allow for the discrimination of one JSON schema from another. In order to resolve this issue the Standard supports content negotiation by profile and defines the `profile` query parameter in the:

- [Requirements class 16: `https://www.opengis.net/spec/ogcapi-processes-1/2.0/req/query-param-profile`](#bb-ogc-api-processes-part1-requirements-queryparamprofile).

conformance class. Using the `profile` query parameter JSON-encoded responses can be requested that conform to a specific JSON schemas.

Three additional conformance classes are specified that extend the basic functionality defined in the *Core* requirements class:

- [Job list](#bb-ogc-api-processes-part1-requirements-joblist) for requesting a list of jobs with optional filtering capabilities,
- [Dismiss](#bb-ogc-api-processes-part1-requirements-dismiss) for cancelling active jobs or deleting completed jobs, and
- [Callback](#bb-ogc-api-processes-part1-requirements-callback) for supporting a callback mechanism to get notification of completed jobs.

Additional capabilities such as support for transactions, extended job monitoring, etc., may be specified in future parts of the OGC API — Processes series or as vendor-specific extensions.

Conformance with this Standard SHALL be checked using all the relevant tests specified in Annex A (normative) of this document. The framework, concepts, and methodology for testing, and the criteria to be achieved to claim conformance are specified in the OGC Compliance Testing Policies and Procedures and the OGC Compliance Testing web site.

**Table 5 — Conformance class URIs**

| Conformance class | URI |
|---|---|
| [Core](#conf-core) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/core](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/core) |
| [OGC Process Description](#conf-ogc-process-description) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/ogc-process-description](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/ogc-process-description) |
| [JSON](#ats-json-definition) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/json](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/json) |
| [HTML](#ats-html-content) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/html](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/html) |
| [OpenAPI Specification](#conf-oas) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas) |
| [OpenAPI Specification 3.0](#conf-oas30) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas30](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas30) |
| [OpenAPI Specification 3.1](#conf-oas31) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas31](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/oas31) |
| [Job list](#conf-job-list) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/job-list](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/job-list) |
| [Callback](#conf-callback) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/callback](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/callback) |
| [Dismiss](#conf-dismiss) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/dismiss](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/dismiss) |
| [Collection Input](#conf-collection-input) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/collection-input](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/collection-input) |
| [Remote Collections](#conf-remote-collections) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/remote-collections](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/remote-collections) |
| [Collection Output](#conf-collection-output) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/collection-output](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/collection-output) |
| [Local Filtering](#conf-local-filtering) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/local-filtering](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/local-filtering) |
| [KVP-encoded Execute](#conf-kvp-execute) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/kvp-execute](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/kvp-execute) |
| [Profile Query Parameter](#conf-query-param-profile) | [https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/query-param-profile](https://www.opengis.net/spec/ogcapi-processes-1/2.0/conf/query-param-profile) |
