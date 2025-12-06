# vendorfiles-action

 Action for updating [vendorfiles](https://github.com/Araxeus/vendorfiles)

## Usage

```yaml
- uses: Araxeus/vendorfiles-action@v1
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    package-manager: yarn
```

## Inputs

* `token` [**Required**] GitHub token for the repository.

* `package-manager` [Optional] command to run before `vendor` command. For example, `yarn` or `npm run`. (default: none)

* `config` [Optional] path to the vendor config file or folder containing the config file. Adds `--config <path>` to the vendor update command. (default: none)

* `before-pr-command` [Optional] command to run before creating a PR. (default: none)

## Full example

```yaml
name: Dependency Updater

permissions:
  contents: read
  pull-requests: write

on:
  schedule:
    - cron: 33 7 * * * # every day at 07:33
  workflow_dispatch: null # allow manual trigger

jobs:
  update-vendors:
    runs-on: ubuntu-latest
    steps:
      - run: bun install

      - name: Run vendor update
        uses: Araxeus/vendorfiles-action@v1
        with:
          token: '${{ secrets.GITHUB_TOKEN }}'
          package-manager: bun
```
