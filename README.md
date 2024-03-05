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

- Wait to update pre-commit hook repos for npm-based packages until they are unpublish-safe
- Group pre-commit hook repos with their respective packages
- Require manual action for additional dependencies (see https://github.com/renovatebot/renovate/issues/20780)

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
