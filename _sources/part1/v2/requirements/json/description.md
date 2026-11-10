This section defines the JSON Requirements Class.

<!-- requirements-class -->

<!-- requirement: json/definition -->

**NOTE:** Responses from the execution endpoint [`/processes/{processID}/execution`](#sec-7.12) may or may not generate JSON depending on the process being executed, the [negotiated execution mode](#sec-7.12.2.2), the negotiated response format (specified using the [HTTP Accept](https://www.rfc-editor.org/rfc/rfc2616#section-14.1) header or the [`f`](#req-kvp-execute-f-definition) query parameter) and the [number of requested outputs](#req-core-process-execute-sync-many-json).

<!-- permission: json/media-types -->
