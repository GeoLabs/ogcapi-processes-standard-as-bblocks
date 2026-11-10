# Overview

<!-- requirements-class -->

This requirements class defines the schema of an `OGC Application Package`.

An `OGC Application Package` is a document that describes a process in sufficient detail so that an implementation of this Standard can dynamically deploy that process and make it accessible via an the processes API defined in [“OGC API — Processes — Part 1: Core”](https://fix.me).

The information contained in an `OGC Application Package` includes:

- A formal description of the process including what inputs the process takes and what outputs the process generates.
- Either an inline or by-reference execution unit which describes the `code` that the server needs to execute whenever the process is invoked.
- Additional resource information the server may require in order to establish an execution environment for the execution unit.

# Schema

<!-- requirement: ogcapppkg/schema -->

# processDescription property

The formal process description (i.e. its inputs, its output, etc.) is provided via the `processDescription` property of the application package.

<!-- requirement: ogcapppkg/process-description -->

<div class="note">

**NOTE:** The `processDescription` property is optional and if it is not included in the application package, the process interface must be inferred from the information in the [execution unit](#sec-7.4).

</div>

# executionUnit property

The execution unit, specified using the [`executionUnit` property](#sec-7.4), describes the code that a processing server must execute whenever a mutable process is invoked.

<!-- requirement: ogcapppkg/executionUnit-schema -->

Conformance classes for two types of execution units are defined in this Standard:

- execution units where the executable code is encapsulated with a container (e.g. Docker),
- execution units encoded as a workflow that is executed by some workflow runner (e.g. CWL).

<!-- recommendation: ogcapppkg/execution-unit-docker -->

<!-- permission: ogcapppkg/other-execution-units -->

The following example illustrates an execution unit where the executable code is encapsulated in a Docker image:

```json
{
  "executionUnit": {
    "type": "docker",
    "value": {
      "image": "mydocker/ndvi:latest",
      "bindings": {
        "inputBindings": {
          "inputImage": {
            "prefix": "inputsImages=",
            "inputSeparator": ","
          }
        },
        "outputBindings": {
          "outputImage": {
            "glob": "$(\"/outputs/ndvi_\" + inputs.inputImage.basename)"
          }
        }
      },
      "deployment": "local",
      "config": {
        "cpuMin": 2,
        "cpuMax": 5,
        "memoryMin": 1,
        "memoryMax": 3
      }
    }
  }
}
```

# Media types in operations

<!-- requirement: ogcapppkg/body -->

<!-- requirement: ogcapppkg/package-response-body -->
