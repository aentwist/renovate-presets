# Contributing

Format files with [Prettier](https://prettier.io/) and use [Conventional Commits](https://www.conventionalcommits.org). To help with this, [npm scripts](https://docs.npmjs.com/cli/v10/using-npm/scripts) and a [pre-commit](https://pre-commit.com/) configuration are provided.

Node.js and Python are used for running the npm scripts and installing pre-commit, respectively. Project Node.js and Python versions are kept in .tool-versions. The recommended installation method is via [asdf](https://asdf-vm.com/).

## `npm` scripts

```shell
asdf install nodejs
npm ci
```

```shell
npm run lint
```

## pre-commit

```shell
asdf install python
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pre-commit install
deactivate
```

## See Also

- Renovate [configuration options](https://docs.renovatebot.com/configuration-options/)
