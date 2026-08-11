# renovate-config

This is a collection of shareable [Renovate](https://docs.renovatebot.com/) config presets.

## Getting started

To use the default preset, extend it in your local `renovate.json` file via:

```json
{
  "extends": ["github>adfinis/renovate-config"]
}
```

This resolves to the [`default.json`](default.json) preset in this repository.

To use a different preset from this repository, reference it by name:

```json
{
  "extends": ["github>adfinis/renovate-config:example"]
}
```

This requires an `example.json` file in this repository, which contains a valid Renovate configuration.

You can validate your configuration by running the following lines locally on your machine:

```bash
npm install -g renovate

renovate-config-validator example.json
```

All presets in this repository are validated automatically by a GitHub Actions workflow.

## Helpful links

* [Default presets](https://docs.renovatebot.com/presets-default/)
* [config:recommended](https://docs.renovatebot.com/presets-config/#configrecommended)
* [Discussion board](https://github.com/renovatebot/renovate/discussions)

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE).
