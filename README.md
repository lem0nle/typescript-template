# typescript-template

![Supported node versions](https://img.shields.io/node/v/husky)

<img align="right" src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Typescript_logo_2020.svg/1200px-Typescript_logo_2020.svg.png" height="120px" alt="typescript logo">

A _minimal_ TypeScript project template for both frontend and backend development.

### Features

- Start a TypeScript project with **best practices**
- Better **developer experience** with formatting, linting and fast testing
- A good starting point for both **frontend and backend** development

### Usage

#### Use Github template

[Use this template](https://github.com/lem0nle/typescript-template/generate) to create your own repo on Github.

#### Create locally

Also, you can create a local project with this template.

```bash
npx degit lem0nle/typescript-template my-ts-project
cd my-ts-project
npm install
```

### Develop a library

If you want to further publish your project as a npm library, you may need some manual modifications to this template.

Modify your `package.json`:

```json
{
  // replace `"private": true` line with these:
  "name": "LIBRARY-NAME",
  "version": "1.0.0",
  "author": "YOUR-NAME-AND-EMAIL",
  "source": "src/index.ts",
  "main": "dist/index.js",
  "module": "dist/index.mjs",
  "types": "dist/index.d.ts",
  "exports": {
    ".": {
      "import": "./dist/index.mjs",
      "require": "./dist/index.js"
    }
  }
  // other fields...
}
```

Then you can build and publish your library. We recommend using [Parcel](https://parceljs.org/getting-started/library/) to build your project for simplicity:

```bash
npm install -D parcel
npx parcel build
```

You can add this to your `scripts` field in `package.json`:

```json
{
  "scripts": {
    // ...
    "build": "parcel build",
    "prepublishOnly": "npm run test && npm run build"
  }
}
```
