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

## GitHub Pages (Temporary)

API's

* https://skribble-freddy.github.io/api-doc/sign_api_v2.html
* https://skribble-freddy.github.io/api-doc/sign_api_v3.html
* https://skribble-freddy.github.io/api-doc/validation_api_v1.html

OpenAPI Files

* https://skribble-freddy.github.io/api-doc/sign_api_v2.yaml
* https://skribble-freddy.github.io/api-doc/sign_api_v3.yaml
* https://skribble-freddy.github.io/api-doc/validation_api_v1.yaml


# Tools

Visual Studio Code Add'in https://marketplace.visualstudio.com/items?itemName=Redocly.openapi-vs-code
