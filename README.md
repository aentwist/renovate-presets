# Renovate Presets

Collection of out-of-the-box [Renovate](https://github.com/renovatebot/renovate) [config presets](https://docs.renovatebot.com/config-presets/) for various PLs, frameworks, and tools

## Getting Started

1. Choose presets for your project
1. Extend them in your Renovate config file

_renovate.json_

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>aentwist/renovate//presets/default"]
}
```

Feel free to combine these with other presets, such as Renovate [default presets](https://docs.renovatebot.com/presets-default/).

## Config Preset Features

### [default](presets/default.json)

`github>aentwist/renovate//presets/default`

- Extends [`config:best-practices`](https://docs.renovatebot.com/presets-config/#configbest-practices), [`:preserveSemverRanges`](https://docs.renovatebot.com/presets-default/#preservesemverranges), and [`:automergeBranch`](https://docs.renovatebot.com/presets-default/#automergebranch)
- Require manual action for major updates
- Automerge minor updates except major version zero

### [gitlab/labels](presets/gitlab/labels.json)

`github>aentwist/renovate//presets/gitlab/labels`

- Add GitLab-style labels to merge requests and Dependency Dashboard issues

### [node](presets/node.json)

`github>aentwist/renovate//presets/node`

- Extends [`npm:unpublishSafe`](https://docs.renovatebot.com/presets-npm/#npmunpublishsafe)
- [`dedupe`](https://docs.npmjs.com/cli/v8/commands/npm-dedupe) after updating
- Only use [LTS node releases](https://github.com/nodejs/Release#release-phases)
- Group jsdom

### pre-commit/\*

- Add a custom manager for `additional_dependencies`\*
- Group pre-commit mirrors / hook repos with their respective packages
- Wait to update pre-commit hook repos for npm-based packages until they are unpublish-safe

<details>
  <summary>*Custom manager for <code>additional_dependencies</code></summary>

Adding handling for `additional_dependencies` to Renovate [is not trivial](https://github.com/renovatebot/renovate/issues/20780#issuecomment-1984977877). Ideally this will be implemented someday. Until then, a custom manager with a regular expression has been implemented to accomplish the same task. For it to match your `additional_dependencies` you must include a special comment above each one.

`# renovate: KEY=VALUE...`

It **MUST** specify the datasource. For example, `datasource=npm`.
<br>
It **MAY** specify the versioning (default: semver). Add a versioning token after the datasource token, delimited by a space. For example, `versioning=pep440`.

Here is a config example,

_.pre-commit-config.yaml_

```yaml
repos:
  - repo: https://github.com/aentwist/pre-commit-mirrors-commitlint
    rev: v19.0.3
    hooks:
      - id: commitlint
        stages: [commit-msg]
        additional_dependencies:
          # renovate: datasource=npm
          - commitlint@19.0.3
          # renovate: datasource=npm
          - "@commitlint/config-conventional@19.0.3"
```

For more information, see [Custom Manager Support using Regex](https://docs.renovatebot.com/modules/manager/regex/#required-fields).

</details>

### [pre-commit/javascript](presets/pre-commit/javascript.json)

`github>aentwist/renovate//presets/pre-commit/javascript`

## Examples

### Vue with pre-commit and GitLab labels

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>aentwist/renovate//presets/default",
    "github>aentwist/renovate//presets/node",
    "github>aentwist/renovate//presets/pre-commit/javascript",
    "github>aentwist/renovate//presets/gitlab/labels"
  ]
}
```

## See Also

- [`ignorePresets`](https://docs.renovatebot.com/configuration-options/#ignorepresets)
