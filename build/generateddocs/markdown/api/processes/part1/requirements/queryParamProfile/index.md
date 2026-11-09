
# Profile query parameter (Requirements-class)

`ogc.api.processes.part1.requirements.queryParamProfile` *v2.0*

Requirements class “Profile query parameter” of OGC API — Processes — Part 1: Core (DRAFT, OGC 18-062r3).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The “Profile query parameter” Requirements Class specifies additional provisions for properties that reference another resource.

<!-- requirements-class -->

Some properties may be represented in multiple representations in the same format, depending on the intended use of the data.

[RFC 6906 The ‘profile’ Link Relation Type](#rfc6906) defines the concept of a profile to support such use cases.

A profile is defined not to alter the semantics of the resource representation itself, but to allow clients to learn about additional semantics (constraints, conventions, extensions) that are associated with the resource representation, in addition to those defined by the media type and possibly other mechanisms.

To request one or more profiles, a query parameter “profile” can be used:

<!-- requirement: query-param-profile/definition -->

<!-- permission: query-param-profile/default -->

Determining the profile(s) of the response is part of the content negotiation process after the proactive content negotiation as specified by the [HTTP RFC](https://www.rfc-editor.org/rfc/rfc9110.html#name-content-negotiation) has been completed. The server determines the applicable profile(s) for the selected media type.

Different media types have different characteristics. A consequence is that it can be impossible to support a profile for a media type or it can be against the design goals of a media type to support a profile.

<!-- permission: query-param-profile/profiles-of-media-type -->

The server will select the profile(s) of the response, if any, from the list of profiles supported for the media type and resource.

<!-- recommendation: query-param-profile/negotiation -->

<!-- requirement: query-param-profile/response -->

<!-- recommendation: query-param-profile/link-header -->

**NOTE:** A set of profile URIs for content defined in this Standard can be found in the [Profile identifiers](#profile-uris) table.

## Sources

* [OGC API - Processes - Part 1: Core](https://docs.ogc.org/DRAFTS/18-062r3.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part1/requirements/queryParamProfile`

