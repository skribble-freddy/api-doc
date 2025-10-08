# Skribble APIs

This repository hosts the Skribble APIs as OpenAPI specs,
prepared for use with [Redocly](https://redocly.com/).

## APIs included
- **Validation API** – v1 (`validation_v1`)
- **Signing API** – v2 (`sign_v2`)
- **Signing API** – v3 (`sign_v3`)

## How to use

### Redocly command line tool

```bash
npx @redocly/cli --help
```

### Lint API specs

```bash
npm run lint
```

### Bundle API specs

Output will be in `dist/`

```bash
npm run bundle
```

### Preview or Build (HTLM) API docs

```bash
npm run build 
npm run build:validation_v1

npm run preview:validation_v1
```

### Folder structure
- `openapi/<api_version>` → Split OpenAPI spec (`openapi.yaml` imports from `paths/` + `components/`)
- `docs/` → Markdown docs (overview, auth, errors, changelog, etc.)


# Tools

OpenAPI Validation https://oas-validation.com/
Visual Studio Code Add'in https://marketplace.visualstudio.com/items?itemName=Redocly.openapi-vs-code

https://github.com/Redocly/redocly-cli-cookbook
https://www.npmjs.com/package/openapi-to-postmanv2/v/4.20.1

https://redocusaurus.vercel.app/docs/getting-started/Installation
https://github.com/PaloAltoNetworks/docusaurus-openapi-docs
  https://github.com/facebook/docusaurus/issues/10556

## Solutions

https://docs.stoplight.io/
https://readme.com/documentation
https://www.mintlify.com/
https://scalar.com/
https://fumadocs.dev/docs/ui/comparisons


## References

https://docs.stripe.com/api
https://developer.paypal.com/api/rest/
