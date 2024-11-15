# Akamai Multi-API SDK Management

This repository provides tooling for managing and releasing SDKs across multiple APIs and languages using Sideko.

## Configuration

APIs are defined in OpenAPI specification format with additional metadata:

```yaml
api:
  - account
  - object-storage
  - vpc

languages:
  python:
    sdk_name: linode_py
  typescript:
    sdk_name: linode_ts

servers:
  - url: https://api.linode.com

modules:
  - path: account
    operations:
      - id: account.get-account
        function_name: list
      - id: account.put-account
        function_name: update
```

## Automated Releases

The SDK release workflow (`.github/workflows/sdk-release.yml`) automatically:

1. Detects changes in API specifications
2. Regenerates affected SDKs
3. Bumps version numbers according to semver
4. Creates GitHub releases (if configured)
5. Publishes packages to respective registries (if configured)

### Version Management

Versions follow semantic versioning:
- MAJOR: Breaking API changes
- MINOR: New features, backwards-compatible
- PATCH: Bug fixes, documentation updates

## Configuration Reference

| Field | Description |
|-------|-------------|
| `api` | List of API services |
| `languages` | Supported languages and SDK names + other configuration |
| `servers` | API urls |
| `modules` | Service definitions and operations with customizations |