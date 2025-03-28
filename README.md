# OCI Model Artifact Specification

This repository contain a draft specification for packaging large language models as OCI artifacts.

The specification defines:
- Guidelines for packaging an LLM packaging as an OCI [image manifest](https://github.com/opencontainers/image-spec/blob/main/manifest.md) following the [artifact guideline](https://github.com/opencontainers/image-spec/blob/main/artifacts-guidance.md).
- Media types and packaging guidelines for the files that together comprise the artifact.
- The schema for a config JSON file that describes the model and it's files.

## Distribution
Artifacts adhering to this specification are distributable by any registry that supports the OCI [distribution specification](https://github.com/opencontainers/distribution-spec).

## Runtime
Models packaged according to this specification may be run by Docker Model Runner or any model runtime that supports this specification. Please note that these artifacts are NOT intended to be run directly by a general-purpose container runtime.

## Motivations
Short term goals (Docker Model Runner):
- Allow users of Docker Model Runner to publish and consume models via existing OCI registries instead of requiring work to integrate with a specific SaaS product or requiring registries to adopt a new model-specific API.
- Distribute model files unencrypted and uncompressed to allow for maximum performance.
- Provide metadata about the model that allows tooling to select the appropriate variant for the given environment.
- Openly document the packaging format used by the Docker Model Runner for the distribution of large language models via OCI registries so that:
  - Anyone may publish Docker Model Runner compatible models.
  - Any OCI registry may identify models that are compatible with the Docker Model Runner.
  - Any OCI registry can display information about the model to users in advance of pulling.

Longer term goals (The Broader Ecosystem):
- Promote interoperability by working with the providers of other model runtimes to converge on a common standard.
- Nurture an ecosystem where models are a first-class citizen instead of a flavor of container (although the model runners themselves may or may not be containerized).