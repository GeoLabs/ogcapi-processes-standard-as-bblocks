**NOTE:** The Open API Requirements Class is abstract. Implementations can only conform to the concrete requirements classes [OpenAPI Specification 3.0](#bb-ogc-api-processes-part1-requirements-oas30) or [OpenAPI Specification 3.1](#bb-ogc-api-processes-part1-requirements-oas31).

# Basic requirements

Servers conforming to this requirements class define their API implementation instance as an OpenAPI Document. Note that this requirements class is not specific to a particular version of the OpenAPI specification. Requirements specific to a particular version are defined in separate, dependent requirements classes.

<!-- requirements-class -->

<!-- requirement: oas/definition -->

The requirements [/req/core/landingpage-success](#req-core-landingpage-success) and [/req/core/api-definition-success](#req-core-api-definition-success) in *Core* require that the API definition documents are referenced from the landing page.

OpenAPI definitions can be created using different approaches. A typical example is the representation of the feature collections. One approach is to use a path parameter `collectionId,` i.e., the API definition has only a single path entry for all feature collections. Another approach is to explicitly define each feature collection in a separate path and without a path parameter, which supports specifying filter parameters or explicit feature schemas per feature collection. Both approaches are valid.

<!-- requirement: oas/oas-impl -->

# Complete definition

<!-- requirement: oas/completeness -->

**NOTE:** Servers that, for example, are access-controlled (see [Security](#sec-11.1.4)), support web cache validation, CORS or that use HTTP redirection will make use of additional HTTP status codes beyond regular codes such as `200` for successful GET requests and `400`, `404` or `500` for error situations. See [Clause 7.5.1](#sec-7.5.1).

Clients must be prepared to receive responses not documented in the OpenAPI definition. For example, additional errors can occur in the transport layer outside of the server.

# Exceptions

<!-- requirement: oas/exceptions-codes -->

**Example — An example exception response object definition**

```yaml
description: An error occurred.
content:
  application/json:
    schema:
      $ref: https://schemas.opengis.net/ogcapi/processes/part1/2.0/openapi/schemas/common-core/exception.yaml
  text/html:
    schema:
      type: string
```

# Security

<!-- requirement: oas/security -->

The OpenAPI specification currently supports the following [security schemes](https://spec.openapis.org/oas/v3.0.3#security-scheme-object):

- HTTP authentication,
- an API key (either as a header or as a query parameter),
- OAuth2’s common flows (implicit, password, application and access code) as defined in RFC6749, and
- OpenID Connect Discovery.
