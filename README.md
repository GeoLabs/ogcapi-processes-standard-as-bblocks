# OGC API — Processes: standards as Building Blocks

This proof of concept authors two draft documents as Building Blocks rather than
as a separate AsciiDoc publication. It does not confer official standard status.

| Document | Edition | Local namespace | Local blocks |
| --- | --- | --- | ---: |
| Part 1: Core (OGC 18-062r3, draft) | 2.0 | `ogc.api.processes.part1.v2.*` | 35 |
| Part 2: Deploy, Replace, Undeploy (OGC 20-044, draft) | 1.0 | `ogc.api.processes.part2.v1.*` | 17 |

The 52 local blocks live under [_sources/part1/v2](_sources/part1/v2) and
[_sources/part2/v1](_sources/part2/v1). [standards.yaml](standards.yaml) defines
both documents, their ordered clauses, nested subclauses and OGC/ModSpec layout.
Building Block `version` fields are revision metadata, not standard editions.

## Imported API components

[bblocks-config.yaml](bblocks-config.yaml) imports the default register and two
public GeoLabs registers:

- [Part 1 API components](https://geolabs.github.io/bblocks-ogcapi-processes/build/register.json):
	175 blocks across independent v1 (73) and v2 (102) namespaces,
	`ogc.api.processes.part1.v1.*` and `ogc.api.processes.part1.v2.*`.
	The upstream register documents official source provenance, the v2 source pin
	`0f9c3d88ccdb1802f6356fd39e7963df7b8dadae` and compatibility aliases.
- [Part 2 API components](https://geolabs.github.io/bblock-ogcapi-processes-part2/build/register.json):
	`ogc.api.processes.part2.v1.*`.

These are imported components, not additional locally authored clauses. Part 1
uses the v2 components. Part 2 uses the v1 components and retains its normative
Core prerequisite `http://www.opengis.net/spec/ogcapi-processes-1/1.0/conf/core`
(OGC 18-062r2), not this repository's Part 1 v2 Core block. Normative conformance
URIs belong in `depends-on`; Building Block identifiers belong in `dependsOn`.

## Automatic standards generation

The normal `bblocks-postprocess` build installs and invokes
`standard_gen.plugin.SpecgenBuildPlugin`, declared under `plugins.build` in
[bblocks-config.yaml](bblocks-config.yaml). No local generator checkout, editable
installation or separate CLI generation step is required.

- Package: `bblocks-specgen @ git+https://github.com/JFarduino/bblocks-specgen@c8b79dc91bca45a592f0eca66fd1df12c39da970`.
- Maintainer context: this is a pinned snapshot of the `feature/update` branch
	from [JFarduino/bblocks-specgen](https://github.com/JFarduino/bblocks-specgen),
	proposed in [upstream PR #2](https://github.com/ogcincubator/bblocks-specgen/pull/2).
	Update the SHA deliberately after review; do not silently substitute an old
	local clone or a moving branch.
- Postprocessor requirement: `bblocks-postprocess` **1.1.8 or later**, including
	build-plugin constructor configuration and the `after_register` lifecycle hook.
	Upstream revision `2deb5c60331691186d997e4f6ae9aab18b548ce5` supports this
	integration. The existing build script uses the moving `latest` image by
	default (`BBP_IMAGE_TAG` can select an image tag); this change pins the plugin,
	not the image, its transitive dependencies or the reusable workflows.
- Configuration: `standards-file: standards.yaml`, `build-dir: build/standards`;
	both paths are relative to the repository root, not to the register file.

The hook consumes the assembled local/imported register at `after_register`,
before the register is written and before semantic uplift. It adds a top-level
`standards` list to the output register with document metadata, repository-relative
paths and published URLs when a `baseURL` is available.

Expected outputs after a successful build:

- `build/standards/index.html`: index of the two documents.
- `build/standards/part1/index.html` and `build/standards/part1/report.json`:
	Part 1 document and inclusion report, expected to cover all 35 local blocks.
- `build/standards/part2/index.html` and `build/standards/part2/report.json`:
	Part 2 document and inclusion report, expected to cover all 17 local blocks.
- Per-document generated styles, assets and generator markers.

The standards output remains under `build/standards` even when the local register
is written under `build-local`. The tracked [standard/index.html](standard/index.html),
the existing documents under [standard/](standard/) and all user CSS are preserved:
this integration neither overwrites them nor changes their navigation links.
The old facade therefore does not automatically point to the new output.

## Build and verification

For an interactive local build, run `./build.sh` from the repository root and
review/approve the plugin permission prompt. [build.sh](build.sh) already mounts
the repository and runs the normal postprocessor; it is unchanged and does not
forward additional command-line arguments. Docker and network access to the
image registry, GitHub/package dependencies and public imported registers are
required. No host Python setup is needed.

For a non-interactive verification, use a disposable snapshot with the same
postprocessor invocation, remove the interactive TTY flags and pass
`--skip-permissions true` **only after reviewing and trusting the plugin**.
Disable SPARQL uploads and template updates for that verification. Do not rely
on `./build.sh --skip-permissions true`: this script does not forward the flag.

Verify current public publications without local URL mappings or sibling mounts:
exclude the ignored local configuration overrides and `.volumes` from the
snapshot. The generator needs no `extra-registers` because the configured imports
are already assembled by the postprocessor. If dependencies are being republished,
publish Part 1 components first, then Part 2 components, then this register.

Check both inclusion reports against the 35 + 17 local blocks, the output
register's two `standards` entries and URLs, and the normal validation reports.
An isolated public-import build on **2026-11-10**, using postprocessor revision
`2deb5c60331691186d997e4f6ae9aab18b548ce5` and the pinned plugin above, passed
**52/52 blocks**. It installed the plugin automatically without either local
generator checkout or sibling URL mappings. Both documents were generated,
their reports loaded **35/35 Part 1** and **17/17 Part 2** blocks, and the register
contained both `standards` entries and their published-target URLs. The generated
HTML had no missing internal anchor targets, duplicate IDs or unresolved
`bblocks://` links. This was a local end-to-end build, not an observed GitHub
Actions deployment.

The generator still emitted **14 abstract-test/requirement matching warnings**
(seven per document). These source-level correspondence issues are not repaired
by configuring the plugin; successful generation does not establish full draft
or runtime conformance. The existing tracked artifacts are historical until CI
regenerates them; they were not replaced by this disposable verification build.
The separately identified CWL test-harness issue is outside this integration;
no schema or fixture is changed here to hide a validation failure.

## CI, publication and plugin trust

- [.github/workflows/process-bblocks.yml](.github/workflows/process-bblocks.yml)
	already uses the same reusable publication workflow as
	[OGC API — Common](https://github.com/JFarduino/ogcapi-common-standards-as-bblocks).
	It builds and publishes the repository root, including `build/standards`; no
	separate generator step is needed. Its existing SPARQL secret forwarding and
	publication permissions are unchanged. Review those settings before running
	the publication workflow if uploads are not desired.
- [.github/workflows/pr-check.yml](.github/workflows/pr-check.yml) uses the
	read-only reusable PR workflow with `contents: read` and no forwarded secrets.
	The checked upstream contract sets `fail_on_error: 'true'`,
	`enable_sparql: 'false'` and `deploy_viewer: 'false'` internally; those settings
	are not exposed as caller inputs. The supported `skip_permissions: 'true'`
	input permits the plugin to run without an interactive prompt.

A build plugin executes third-party code and installs dependencies; a pinned SHA
reduces accidental drift but does not make that code safe. Review changes to
plugin configuration and dependencies, keep PR validation unprivileged, and do
not switch it to `pull_request_target` or expose publication secrets to untrusted
PR code. Permission skipping is an explicit trust decision, not a sandbox or
an alternative to review. The workflows still follow upstream `master` and the
publication build is privileged, so maintainers must review upstream changes too.
