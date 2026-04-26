# formae-plugin-standard

Orbital metapackage that pulls in the default set of [formae](https://github.com/platform-engineering-labs/formae) plugins.

`formae plugin install standard` installs:

- [aws](https://github.com/platform-engineering-labs/formae-plugin-aws)
- [azure](https://github.com/platform-engineering-labs/formae-plugin-azure)
- [gcp](https://github.com/platform-engineering-labs/formae-plugin-gcp)
- [oci](https://github.com/platform-engineering-labs/formae-plugin-oci)
- [ovh](https://github.com/platform-engineering-labs/formae-plugin-ovh)
- [auth-basic](https://github.com/platform-engineering-labs/formae-plugin-auth-basic)

The orbital solver pulls each plugin in at its latest available version in the requested channel. Pinning a specific version of `standard` does not pin the underlying plugins — to pin a plugin, install it explicitly:

```bash
formae plugin install standard
formae plugin install aws@0.1.5    # override the version pulled in by standard
```

## How it builds

Pushing a tag (`X.Y.Z` or `X.Y.Z-dev[.N]`) triggers `.github/workflows/release.yml`, which dispatches `formae-actions/plugin-build.yml` with `kind=metapackage`. The dispatched workflow signs the metapackage with the `platform.engineering` intermediate cert and publishes it to the `community` orbital repo.

This repo holds no signing material — only a fine-grained PAT (`HUB_DISPATCH_PAT`) scoped to `actions:write` on `formae-actions`, set as a repo secret.

## License

[FSL-1.1-ALv2](LICENSE)
