# Model Format Specification

## Media Types

### Config File
- `application/vnd.docker.ai.model.config.v1+json` - Model artifact configuration file in JSON format.

### Layers
- `application/vnd.docker.ai.gguf` - Raw GGUF file containing model weights or LoRA adapter.
- `text/plain` - Raw file containing plain text data. This is used for licenses, templates, and other text files.

## Example Manifest

```json
{
  "schemaVersion": 2,
  "mediaType": "application/vnd.oci.image.manifest.v1+json",
  "config": {
    "mediaType": "application/vnd.docker.ai.model.config.v1+json",
    "size": 363,
    "digest": "sha256:9f0dd517363df0d9f57fccf2599eb56c9276721e874167d2e31959669a13ec17"
  },
  "layers": [
    {
      "mediaType": "`application/vnd.docker.ai.gguf",
      "size": 637699456,
      "digest": "sha256:2af3b81862c6be03c769683af18efdadb2c33f60ff32ab6f83e42c043d6c7816"
    },
    {
      "mediaType": "text/plain",
      "size": 13,
      "digest": "sha256:d0ce8fae4da6de6e5a4b85ebee156ac8f3ab6d8407caf4493968d34e9bc3939e"
    }
  ]
}
```

