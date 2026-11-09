
# Docker input binding (Schema)

`ogc.api.processes.part2.schemas.inputBinding` *v1.0.0*

How a process input is passed to a Docker execution unit (Requirement /req/docker/input-binding).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

How a process input is passed to a Docker execution unit (Requirement /req/docker/input-binding).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

## Schema

```yaml
type: object
description: ". Defines how to specify the input for the execution unit.\n. The value
  of various properties defined below can be expressions.\n    . The expression language
  SHALL be JavaScript(???).\n. The \"$(...)\" syntax can be used to reference the
  current input or other\n  process inputs in an expression.\n  . The value \"self\"
  refers to the value of the current input.\n  . The value \"inputs.<other_input>\"
  refers to the value of another\n    process input.\n  . If the input is defined
  as a string of format \"file\" or \"directory\"\n    then the meta-values \".path\",
  \".basename\", \".nameroot\" and \".nameext\"\n    can be used to manipulate file
  or directory name without having to\n    resort to complex regular expressions.\n
  \     . \".path\" returns the path of a file name without the file name\n      .
  \".basename\" returns the name of the file without the path\n      . \".nameroot\"
  returns the basename without any extension\n      . \".nameext\" returns the extension
  of the basename"
properties:
  prefix:
    description: Command line prefix to add before the value.
    type: string
  position:
    description: ". The zero-based sorting key.\n. The value can be an integer or
      a string.\n. If the value is a string then it should be an expression that evaluates\n
      \ to a single integer value or null."
    oneOf:
    - type: integer
    - type: string
  valueFrom:
    description: ". If valueFrom is a constant string value, use this as the value.\n.
      If valueFrom is an expression, evaluate the expression to yield the\n  actual
      value to use to build the command line.\n. If the value of the associated input
      parameter is null, valueFrom is\n  not evaluated and nothing is added to the
      command line."
    type: string
  itemSeparator:
    description: 'Join the array elements into a single string with the elements separated

      by itemSeparator.'
    type: string
  shellQuote:
    description: ". A Boolean that controls whether the value is quoted on the command.\n.
      A value of true (or if shecllQuote is not provided) means that the\n  implementation
      SHALL not permit the interpretation of any shell\n  metacharacters or directives.\n.
      A value of false should be used to inject metacharacters for operations\n  such
      as pipes."
    type: boolean
additionalProperties: true
x-bblocks-metadata:
  itemIdentifier: ogc.api.processes.part2.schemas.inputBinding
  register: https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/register.json
  version: 1.0.0
  dateOfLastChange: '2026-11-07'

```

Links to the schema:

* YAML version: [schema.yaml](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/inputBinding/schema.json)
* JSON version: [schema.json](https://geolabs.github.io/ogcapi-processes-standard-as-bblocks/build/annotated/api/processes/part2/schemas/inputBinding/schema.yaml)

## Sources

* [OGC API - Processes - Part 2: Deploy, Replace, Undeploy](https://docs.ogc.org/DRAFTS/20-044.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks](https://github.com/GeoLabs/ogcapi-processes-standard-as-bblocks)
* Path: `_sources/part2/schemas/inputBinding`

