# Model Format Specification

## Media Types

### Config File
- `application/vnd.docker.ai.model.config.v0.1+json` - Model artifact configuration file in the [model config JSON](config.md) format.

### Layers
All layers blobs SHOULD contain the contents of a single file. Layers SHOULD NOT be compressed.

- `application/vnd.docker.ai.gguf.v3` - A file adhering to version 3 of the [GGUF specification](https://github.com/ggml-org/ggml/blob/master/docs/gguf.md), containing a tensor model.
- `application/vnd.docker.ai.gguf.v3.lora` - A file adhering to version 3 of the GGUF specification, containing a LoRA adapter.
- `application/vnd.docker.ai.gguf.v3.mmproj` - A file containing multimodal projector weights in GGUF format, used to bridge vision and language models by projecting visual features into the language model's embedding space.
- `application/vnd.docker.ai.license` - Plain text file containing a software license.
- `application/vnd.docker.ai.chat.template.jinja` – A text file containing a [Jinja](https://jinja.palletsprojects.com/en/stable/) prompt template, used to define chat/inference formatting.

## Example Manifest

```json
{
  "schemaVersion": 2,
  "mediaType": "application/vnd.oci.image.manifest.v1+json",
  "config": {
    "mediaType": "application/vnd.docker.ai.model.config.v0.1+json",
    "size": 363,
    "digest": "sha256:9f0dd517363df0d9f57fccf2599eb56c9276721e874167d2e31959669a13ec17"
  },
  "layers": [
    {
      "mediaType": "application/vnd.docker.ai.gguf.v3",
      "size": 637699456,
      "digest": "sha256:2af3b81862c6be03c769683af18efdadb2c33f60ff32ab6f83e42c043d6c7816"
    },
    {
      "mediaType": "application/vnd.docker.ai.license",
      "size": 13,
      "digest": "sha256:d0ce8fae4da6de6e5a4b85ebee156ac8f3ab6d8407caf4493968d34e9bc3939e"
    }
  ]
}
```
