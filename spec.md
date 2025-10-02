# Model Format Specification

## Media Types

### Config File
- `application/vnd.docker.ai.model.config.v0.1+json` - Model artifact configuration file in the [model config JSON](config.md) format.

### Layers
All layers blobs SHOULD contain the contents of a single file. Layers SHOULD NOT be compressed.

- `application/vnd.docker.ai.gguf.v3` - A file adhering to version 3 of the [GGUF specification](https://github.com/ggml-org/ggml/blob/master/docs/gguf.md), containing a tensor model.
- `application/vnd.docker.ai.gguf.v3.lora` - A file adhering to version 3 of the GGUF specification, containing a LoRA adapter.
- `application/vnd.docker.ai.gguf.v3.mmproj` - A file containing multimodal projector weights in GGUF format, used to bridge vision and language models by projecting visual features into the language model's embedding space.
- `application/vnd.docker.ai.safetensors` - A file adhering to the [safetensors specification](https://github.com/huggingface/safetensors), a safe and fast serialization format for machine learning tensors.
- `application/vnd.docker.ai.vllm.config.tar` - A tar archive containing configuration files (*.json) and metadata files (e.g., merges.txt) used by inference engines.
- `application/vnd.docker.ai.license` - Plain text file containing a software license.
- `application/vnd.docker.ai.chat.template.jinja` - A text file containing a [Jinja](https://jinja.palletsprojects.com/en/stable/) prompt template, used to define chat/inference formatting.

### Sharded Models
Both GGUF and safetensors formats support sharded models where the model weights are split across multiple files. In such cases:
- Multiple layers with the same media type (e.g., `application/vnd.docker.ai.safetensors` or `application/vnd.docker.ai.gguf.v3`) represent different shards of the same model.
- The order of layers in the manifest defines the shard sequence.
- Shards typically follow naming conventions such as `model-00001-of-00002.safetensors` or `model-00001-of-00002.gguf`.

## Example Manifests

### GGUF Model
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

### Safetensors Model (Sharded)
```json
{
  "schemaVersion": 2,
  "mediaType": "application/vnd.oci.image.manifest.v1+json",
  "config": {
    "mediaType": "application/vnd.docker.ai.model.config.v0.1+json",
    "size": 465,
    "digest": "sha256:2ea258562df7df57407d739f3215419dd1827093d4a8057386b0c723fa011305"
  },
  "layers": [
    {
      "mediaType": "application/vnd.docker.ai.safetensors",
      "size": 3968658944,
      "digest": "sha256:67347b23fb4165b652eb6611f5e1f2a06dfcddba8e909df1b2b0b1857bee06c2"
    },
    {
      "mediaType": "application/vnd.docker.ai.safetensors",
      "size": 2203268048,
      "digest": "sha256:a40d941d0e7e0b966ad8b62bb6d6b7c88cce1299197b599d9d0a4ce59aabfc1d"
    },
    {
      "mediaType": "application/vnd.docker.ai.vllm.config.tar",
      "size": 11530752,
      "digest": "sha256:5acfb0cc82593273b8c9032239bbe897b80d17b185d8e7ae148afe21cb188067"
    },
    {
      "mediaType": "application/vnd.docker.ai.license",
      "size": 13,
      "digest": "sha256:d0ce8fae4da6de6e5a4b85ebee156ac8f3ab6d8407caf4493968d34e9bc3939e"
    }
  ]
}
```
