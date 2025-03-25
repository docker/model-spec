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

      The packaging format of the model file(s). Currently the only supported value is `gguf`.

    - **format_version**: string, OPTIONAL

      The version of the packaging `format`.

        - **gguf**: object, OPTIONAL

          Contains metadata specific to the `gguf` format. All fields SHOULD correspond directly to the
          standardized [key-value pairs](https://github.com/ggml-org/ggml/blob/master/docs/gguf.md#general) defined in
          the GGUF specification.

    - **size**: string, REQUIRED

      The total size of the model in bytes.


- **files**: array of objects, REQUIRED

  Lists the files the comprise the model.
    - **diffID**: string, REQUIRED

      The digest of the file contents in the form `<alg>:<hash>`.
    - **type**: string, REQUIRED

      The media type of the file. This indicates the type of the file and how it should be interpreted.

## Example

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

