# Model Artifact Configuration

This section defines the `application/vnd.docker.ai.model.config.v1+json` media type.

## Example

```json
{
  "descriptor": {
    "createdAt": "2025-01-01T00:00:00Z",
    "authors": [
      "xyz@xyz.com"
    ],
    "organization": "XYZ Corp.",
    "name": "xyz-3-8B-Instruct",
    "version": "3.1",
    "title": "XYZ 3 8B Instruct",
    "description": "xyz is a large language model.",
    "docURL": "https://www.xyz.com/get-started/",
    "source": {
      "repoURL": "https://github.com/xyz/xyz3",
      "revision": "1234567890"
    },
    "licenses": [
      "Apache-2.0"
    ]
  },
  "config": {
    "architecture": "llama",
    "format": "gguf",
    "parameter_count": "1.10 B",
    "quantization": "Q4_0",
    "size": "635992801" 
  },
  "files": [
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "model"
    },
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "license"
    },
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "lora"
    },
    {
      "diffID": "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
      "type": "template"
    }
  ]
}
```

