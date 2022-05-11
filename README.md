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

[Use this template](https://github.com/lem0nle/typescript-template/generate) to create your own repo on Github. Run the following commands to start:

```bash
npm i -g pnpm  # if you haven't already
pnpm i
```

#### Create locally

Also, you can create a local project with this template.

```bash
npx degit lem0nle/typescript-template my-ts-project
cd my-ts-project
pnpm i
```

### Develop a library

If you want to further publish your project as a npm library, you may need some manual modifications to this template.

Modify your `package.json`:

```json
{
  // replace `"private": true` line with these:
  "name": "LIBRARY-NAME",
  "version": "0.1.0",
  "author": "YOUR-NAME-AND-EMAIL",
  "repository": {
    "type": "git",
    "url": "YOUR-GIT-REPOSITORY"
  },
  "type": "module",
  "source": "src/index.ts",
  "main": "dist/index.js",
  "types": "dist/index.d.ts"
  // other fields...
}
```

Then you can build and publish your library. We recommend using [Parcel](https://parceljs.org/getting-started/library/) to build your project for simplicity:

```bash
pnpm i -D parcel
npx parcel build
```

You can add this to your `scripts` field in `package.json`:

```json
{
  "scripts": {
    // ...
    "build": "parcel build",
    "prepublishOnly": "npm run build && npm run test"
  }
}
```

### Release your library manually

Whenever you feel ready, you can publish your package to [npmjs.com](https://npmjs.com) for public access (tests will be run before publishing automatically):

```bash
npm login
npm publish --access=public
```

After it succeeds, you can tag your release with the version number specified in `package.json`:

```bash
git tag v0.1.0 -m v0.1.0
git push && git push --tags
```

### Automatic release with `semantic-release`

Optionally, you can configure your project to trigger automatic release each time the main branch is updated (pushed or merged). Version numbers will be calculated based on [conventional commit messages](https://www.conventionalcommits.org/en/v1.0.0/). Consult [semantic-release documentation](https://github.com/semantic-release/semantic-release) for more information.

Before you make these changes, make sure you manually published your package at least once as described previously.

Install `semantic-release` and several plugins:

```bash
pnpm i -D semantic-release @semantic-release/changelog @semantic-release/git
```

Modify `package.json`:

```json
{
  // ...
  "release": {
    "branches": ["main"],
    "plugins": [
      "@semantic-release/commit-analyzer",
      "@semantic-release/release-notes-generator",
      "@semantic-release/changelog",
      "@semantic-release/npm",
      "@semantic-release/git",
      "@semantic-release/github"
    ]
  }
}
```

Modify `.github/workflows/CI.yaml`:

```yaml
jobs:
  build:
    steps:
      # ...
      - name: Semantic Release
        uses: cycjimmy/semantic-release-action@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

Remember to set `NPM_TOKEN` in your GitHub repository settings (Settings -> Secrets -> Actions -> New repository secret) before you push these changes.
