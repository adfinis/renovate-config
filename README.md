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

## Presets

All presets besides `default` are opt-in and designed to be combined. None of
them enable automerge; every PR still needs a human to merge it.

| Preset | Description |
|---|---|
| [`groups-minor-patch`](groups-minor-patch.json) | Group all minor and patch updates into one PR per ecosystem. |
| [`groups-digests`](groups-digests.json) | Group all digest, pin and pinDigest updates into a single PR. |
| [`groups-ecosystems`](groups-ecosystems.json) | Apply Renovate's upstream-maintained dependency family groups. |
| [`schedule-weekly`](schedule-weekly.json) | Create and update PRs only early Monday morning. Open PRs are not rebased or updated outside that window. |
| [`schedule-monthly`](schedule-monthly.json) | Create and update PRs only early on the first day of the month. Open PRs are not rebased or updated outside that window. |
| [`limits-strict`](limits-strict.json) | Tight limits on how many Renovate PRs and branches may exist at once, and how many PRs are opened per hour. |
| [`limits-relaxed`](limits-relaxed.json) | Moderate limits on how many Renovate PRs and branches may exist at once, and how many PRs are opened per hour. |
| [`rebase-conflicted`](rebase-conflicted.json) | Only rebase PRs when they actually conflict, and never re-create PRs that were closed by a human. |
| [`dashboard-approval-majors`](dashboard-approval-majors.json) | Major updates are only listed on the Dependency Dashboard and become PRs once approved there. |
| [`lockfile-maintenance`](lockfile-maintenance.json) | Refresh lock files monthly in a single PR that must first be approved on the Dependency Dashboard. |
| [`quiet`](quiet.json) | Low-noise bundle: ecosystem groups, one non-major PR per manager, one digest PR, weekly schedule, rebase only on conflict, relaxed limits. |

### Recommended config

```json
{
  "extends": [
    "github>adfinis/renovate-config",
    "github>adfinis/renovate-config:quiet"
  ]
}
```


Notes:

* Put the presets **after** `github>adfinis/renovate-config` so they override its `schedule:nonOfficeHours`.
* The schedule presets use the `timezone` from the default preset (`Europe/Zurich`). Set `timezone` yourself if you don't extend the default.
* `dashboard-approval-majors` requires the Dependency Dashboard, which `config:recommended` (and therefore the default preset) enables.
* Security updates (`vulnerabilityAlerts`) are not affected by the grouping and schedule presets: Renovate always creates them individually and immediately.

### Stability days

None of these presets set `minimumReleaseAge`, `internalChecksFilter` or
`prCreation`, so they compose with the stability-days behaviour from
`config:best-practices` (or your own `minimumReleaseAge`). Renovate filters
versions that are younger than `minimumReleaseAge` *before* grouping, so a
grouped PR only ever contains releases that have passed the waiting period.

Lock file maintenance is the exception: it refreshes the whole lock file with
the package manager and therefore upgrades transitive dependencies regardless of
`minimumReleaseAge`. It is not part of `quiet`. The [`lockfile-maintenance`](lockfile-maintenance.json)
preset offers it anyway, but only monthly and only after a human approves the
PR on the Dependency Dashboard.

## Helpful links

* [Default presets](https://docs.renovatebot.com/presets-default/)
* [config:recommended](https://docs.renovatebot.com/presets-config/#configrecommended)
* [Discussion board](https://github.com/renovatebot/renovate/discussions)

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE).
