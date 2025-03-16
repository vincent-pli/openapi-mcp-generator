# Publishing to npm

This document contains instructions for publishing this package to npm.

## Prerequisites

1. You need an npm account. Sign up at https://www.npmjs.com/ if you don't have one.
2. You need to be logged in to npm from your command line.

## Steps to Publish

1. **Ensure your code is ready for publishing**
   - Make sure all necessary files are included (and unnecessary ones excluded via .npmignore)
   - Verify that the package.json is correctly configured

2. **Make the main script executable**
   ```bash
   chmod +x src/index.js
   ```

3. **Login to npm (if you haven't already)**
   ```bash
   npm login
   ```

4. **Publish to npm**
   ```bash
   npm publish
   ```

5. **For future updates**
   - Update the version number in package.json
   - Run `npm publish` again

## Setting up GitHub Actions for Automatic Publishing (Optional)

You can set up a GitHub workflow to automatically publish to npm when you create a new release.

1. Create a GitHub secret called `NPM_TOKEN` with your npm token
2. Create a file at `.github/workflows/publish-npm.yml` with the following content:

```yaml
name: Publish to npm

on:
  release:
    types: [created]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18.x'
          registry-url: 'https://registry.npmjs.org/'
      - run: npm ci
      - run: chmod +x src/index.js
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{secrets.NPM_TOKEN}}
```

## Verifying Publication

After publishing, you can verify that your package is available on npm by visiting:
https://www.npmjs.com/package/openapi-mcp-generator
