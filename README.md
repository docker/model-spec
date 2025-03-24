# OCI Model Artifact Specification

This repository contain a draft specification for packaging large language models as OCI artifacts.


The specification defines:
- Guidelines for packaging an LLM packaging as an OCI [image manifest](https://github.com/opencontainers/image-spec/blob/main/manifest.md) following the [artifact guideline](https://github.com/opencontainers/image-spec/blob/main/artifacts-guidance.md).
- Media types and packaging guidelines for the files that together comprise the artifact.
- The schema for a config JSON file that describes the model and it's files.

## Distribution
Artifacts adhering to this specification are distributable by any registry that supports the OCI [distribution specification](https://github.com/opencontainers/distribution-spec).

## Runtime
Models packaged according to this specification may be run by any model runtime that supports this specification. Please note that these artifacts are not intended to be run directly by a general-purpose [container runtime](https://github.com/opencontainers/runtime-spec).