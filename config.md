# Model Artifact Configuration

This section defines the `application/vnd.docker.ai.model.config.v0.1+json` media type, otherwise known as a model
config JSON file. Model config JSON files MUST be valid JSON objects.

## Fields

- **descriptor** object, OPTIONAL

  Describes the provenance of the artifact. It may contain any of the following fields:
    - **createdAt**: string, OPTIONAL

      The time the artifact was created.


- **config**: object, REQUIRED

  Contains metadata describing the model.
    - **format**: string, REQUIRED

      The packaging format of the model file(s). Supported values are `gguf` and `safetensors`.

    - **format_version**: string, OPTIONAL

      The version of the packaging `format`.

        - **gguf**: object, OPTIONAL

          Contains metadata specific to the `gguf` format. All fields SHOULD correspond directly to the
          standardized [key-value pairs](https://github.com/ggml-org/ggml/blob/master/docs/gguf.md#general) defined in
          the GGUF specification.

        - **safetensors**: object, OPTIONAL

          Contains metadata specific to the `safetensors` format. May include fields such as:
          - **architecture**: string, OPTIONAL - The model architecture (e.g., "llama", "qwen2", "mistral")
          - **parameter_count**: string, OPTIONAL - The total number of parameters (e.g., "7.24 B", "13 B")


    - **size**: string, REQUIRED

      The total size of the model in bytes.


- **files**: array of objects, REQUIRED

  Lists the files the comprise the model.
    - **diffID**: string, REQUIRED

      The digest of the file contents in the form `<alg>:<hash>`.
    - **type**: string, REQUIRED

      The media type of the file. This indicates the type of the file and how it should be interpreted.

## Examples

### GGUF Model

```json
{
  "descriptor": {
    "createdAt": "2025-01-01T00:00:00Z"
  },
  "config": {
    "format": "gguf",
    "format_version": "3",
    "gguf": {
      "architecture": "llama",
      "parameter_count": "1.10 B",
      "quantization": "Q4_0"
    },
    "size": "635992801"
  },
  "files": [
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "application/vnd.docker.ai.gguf.v3"
    },
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "application/vnd.docker.ai.license"
    },
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "application/vnd.docker.ai.gguf.v3.lora"
    }
  ]
}
```

### Safetensors Model (Sharded)

```json
{
  "descriptor": {
    "createdAt": "2025-01-01T00:00:00Z"
  },
  "config": {
    "format": "safetensors",
    "safetensors": {
      "architecture": "qwen2",
      "parameter_count": "3.09 B"
    },
    "size": "6171926992"
  },
  "files": [
    {
      "diffID": "sha256:67347b23fb4165b652eb6611f5e1f2a06dfcddba8e909df1b2b0b1857bee06c2",
      "type": "application/vnd.docker.ai.safetensors"
    },
    {
      "diffID": "sha256:a40d941d0e7e0b966ad8b62bb6d6b7c88cce1299197b599d9d0a4ce59aabfc1d",
      "type": "application/vnd.docker.ai.safetensors"
    },
    {
      "diffID": "sha256:5acfb0cc82593273b8c9032239bbe897b80d17b185d8e7ae148afe21cb188067",
      "type": "application/vnd.docker.ai.vllm.config.tar"
    },
    {
      "diffID": "sha256:d0ce8fae4da6de6e5a4b85ebee156ac8f3ab6d8407caf4493968d34e9bc3939e",
      "type": "application/vnd.docker.ai.license"
    }
  ]
}
```
