# Skribble APIs – Documentation Repo

This repository hosts the Skribble APIs as OpenAPI 3.0 specs, prepared for use with [Redocly](https://redocly.com/).

## APIs included
- **Validation API** – v1 (`validation_v1`)
- **Signing API** – v2 (`sign_v2`)
- **Signing API** – v3 (`sign_v3`, upcoming placeholder)

## How to use

### Preview API docs
```bash
npx @redocly/cli preview-docs openapi/validation_v1/openapi.yaml
npx @redocly/cli preview-docs openapi/sign_v2/openapi.yaml
```

### Lint API specs
```bash
npx @redocly/cli lint openapi/validation_v1/openapi.yaml
```

### Folder structure
- `openapi/<api_version>` → Split OpenAPI spec (`openapi.yaml` imports from `paths/` + `components/`)
- `docs/` → Markdown docs (overview, auth, errors, changelog, etc.)
