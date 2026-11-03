# Adobe for Developers plugin documentation

This repository contains the documentation website for the Adobe for Developers
plugin, including installation guidance, tool and skill references, release notes,
and support information. It contains the documentation, not the plugin implementation.

## Requirements

- Node.js matching the `^24.11.0` requirement in [package.json](package.json).
- npm, included with Node.js.
- Internet access to download the Adobe Developer Site tooling used by the npm scripts.

## Run locally

From the repository root, start the documentation preview:

```sh
npm run dev
```

Once the server is ready, open:

<http://localhost:3000/adobe-for-developers/>

This is the default local URL. If port 3000 is already in use, use the port
reported by the development server and keep the `/adobe-for-developers/` path.
Stop the server with `Ctrl+C` in the terminal where it is running.

## Edit the documentation

Page content is in [src/pages](src/pages):

- [Landing page](src/pages/index.md)
- [Getting started](src/pages/guides/index.md) and [Claude installation guide](src/pages/guides/quick-start/claude.md)
- [Tool reference](src/pages/guides/reference.md)
- [Skills](src/pages/guides/skills.md)
- [Changelog](src/pages/guides/changelog.md)
- [Support](src/pages/support/index.md) and [FAQ](src/pages/support/faq.md)

Update [src/pages/config.md](src/pages/config.md) when changing navigation.
The same file defines the site's `/adobe-for-developers/` base path.
Shared images are in [src/pages/assets](src/pages/assets).

## Check changes

Run the existing documentation linter:

```sh
npm run lint
```

To check internal and external links:

```sh
npm run link:checkAllLinks
```

These commands use the Adobe Developer Site tooling and require internet access.

## Contributing

See the [contribution guidelines](.github/CONTRIBUTING.md) and
[Code of Conduct](CODE_OF_CONDUCT.md) before submitting changes.
For documentation issues, use the
[repository issue tracker](https://github.com/AdobeDocs/one-adp-connector-docs/issues).

For details about the shared website tooling, see the
[ADP Developer Site documentation](https://developer-stage.adobe.com/dev-docs-reference/).
