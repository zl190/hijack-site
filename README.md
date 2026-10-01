# Hijack website

The bilingual website for [Hijack](https://github.com/zl190/hijack), a macOS menu bar app for voice input.

**Live site:** [hijack.ylab3.com](https://hijack.ylab3.com/)

**App source, installation and releases:** [zl190/hijack](https://github.com/zl190/hijack)

## Develop

Requires Node.js 22 or later. Install the locked dependencies, validate the site and start a local preview:

```sh
npm ci
npm run check
python3 -m http.server 4173 --bind 127.0.0.1 --directory dist
```

Open `http://127.0.0.1:4173/` for Chinese or `http://127.0.0.1:4173/?lang=en` for English. Re-run `npm run build` after editing source files.

`index.html` owns the shared page structure, `locales.js` owns localized content, and `home.js` owns the interactive demonstration. `scripts/build-site.mjs` copies an explicit list of public files into `dist/` and rejects stale CSS/JS fingerprints. Drafts and documentation are excluded from deployment.

## Deploy

```sh
npm run deploy:cf
```

Wrangler must already be authenticated for the account in `wrangler.jsonc`. The configuration retains the existing `hijack-site` Worker and `hijack.ylab3.com` custom domain. `npm run check` validates a dry-run deployment; it does not publish.

Git-backed automatic builds are not yet verified: the Cloudflare Builds management API returned HTTP 401 during migration. Until that connection is configured, deploy explicitly from this repository.

## Content and artwork

See [website documentation](docs/website.md) for routes, localization, demonstration behavior, caching and asset provenance. [Brand assets](assets/brand/README.md) document the wordmark. The [original implementation review](docs/legacy-review.md) is retained as a historical record.

The directory listing and card at [apps.ylab3.com](https://apps.ylab3.com/) belong to [zl190/ylab-gallery](https://github.com/zl190/ylab-gallery).

## Repository split

Website history was extracted from the `site/` directory of [zl190/hijack](https://github.com/zl190/hijack) at commit `724ece4496df649753340cba949782e50b8ba326`. Build configuration and this maintenance entry were added here. The app, installers and releases remain in the app repository.

## License

[MIT](LICENSE) for project code and original artwork. Third-party imagery has separate [provenance](docs/website.md#assets-and-cache) and is not covered by that license.
