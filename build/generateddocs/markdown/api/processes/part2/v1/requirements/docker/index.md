
# Docker (Requirements-class)

`ogc.api.processes.part2.v1.requirements.docker` *v1.0.0*

Conformance class for OGC API - Processes Part 2 (DRAFT). Defines requirements for Docker-based execution units in OGC Application Packages.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Overview

<!-- requirements-class -->

This clause defines the requirements for describing, in the execution unit of an [OGC Application Package](#sec-7), a processes’ executable code encapsulated in a Docker container.

# Schema

<!-- requirement: docker/schema -->

# Properties type and image

<!-- requirement: docker/execution-unit -->

# Property deployment

<!-- requirement: docker/deployment -->

# Property config

<!-- requirement: docker/config -->

# Property bindings

## Overview

<!-- requirement: docker/bindings -->

<div class="note">

**NOTE:** If a binding information is not specified, it is assumed that the processing server will apply some internally-defined default mapping; this is an implementation detail and beyond the scope of this Standard.

</div>

## Input binding

### Overview

<!-- requirement: docker/input-binding -->

The following input binding parameters can be specified:

- **prefix**:

  - A prefix to be added before an argument value that is used for the execution unit invocation.

- **position**:

  - The value can be an integer or a string.
  - If it is an integer then it is assumed to be 0-based and the argument is added in this position to the execution unit invocation.
  - If the value is a string then it should be an expression that evaluates to single integer value or null.
  - If the value expression evaluates to null, nothing is added to the execution unit invocation.

- **valueFrom**:

  - If the `valueFrom` is a constant string value then this value is added verbatim as an argument to the execution unit invocation.
  - If the `valueFrom` is an expression, evaluate the expression to yield the actual value and add that as an argument to the execute unit invocation.
  - If the `valueFrom` is null, nothing is added to the execution unit invocation.

- **itemSeparator**

  - Join the array elements into a single string with the elements separated by the `itemSeparator` and add that as an argument to the execution unit invocation.

- **shellQuote**

  - A boolean that controls whether the value used as an argument in the execution unit invocation is quoted or not.
  - A value of `true` (the default value) means metacharacters or directives are not interpreted when the execution unit is invoked.
  - If metacharacters or directives need to be specified when the execution unit is invoked the value of this parameter should be set to `false`.

### Macro substitution in expressions

The value of a binding parameters can be an expression.

<!-- requirement: docker/expression-lang -->

The macro syntax “$(…​)” can be used to reference an process input value in an expression.

- The value `self` (e.g. `$(self)`) refers to the value of the current process input in the current execution unit invocation.

- The value `inputs.<other_input>` (e.g. `$(inputs.arg2)`) refers to the value of another process input in the current execution unit invocation.

- If the input is defined as a string type of format “file” or “directory”, the following meta-values can be used to manipulate the file or directory path without having to resort to complex regular expressions.

  - “.path” returns the path of a name without the basename
  - “.basename” returns the name of the file or directory without the path
  - “.nameroot” returns the basename with any extension
  - “.nameext” return the extension of the basename

## Output binding

<!-- requirement: docker/output-binding -->

The optional `glob` parameter can be used in an output binding to define a wildcard pattern to find the output on a disk or a mounted volume.

The same [macro expressions](#sec-8.6.2.2) that can be used in an input binding expression can also be used with `glob` expressions.

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/v1/requirements/docker`

