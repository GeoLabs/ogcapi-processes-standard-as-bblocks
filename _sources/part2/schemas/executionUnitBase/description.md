One execution unit: a link, or a qualified value holding a container image, a CWL document or a custom type.

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- The draft refers to `../cwl/cwl.yaml`, which it does not include. This block uses the CWL v1.2 schema URL that the draft gives in a comment.
- As written in the draft, the third `anyOf` branch accepts any `type`, so this schema does not reject an invalid Docker `value`. Validate such a value against `ogc.api.processes.part2.schemas.executionUnitContainer`.
