# 🚀 Auto-Pypi Action

This is a GitHub Action to bump, create a tag, and deploy to pypi

## ❔ How to Use

1. First ensure that you have an API token in the secrets, as ``TWINE_USERNAME``
2. Make a ``bumpver.toml`` file to contain all the versions to be updated and the version pattern (look at the ``bumpver.toml`` example)
3. When making a Pull Request simply place the string "version: " followed by either "major", "minor", or "patch" in the description, depending on what you want to bump.
4. This is will bump the version, make a new tag, and deploy it to PyPi

## 🏞️ Workflow

A sample workflow that bumps, makes a new tag, and deploys it to PyPi on merge.

### Requirements

1. write contents permission (to bump and push)
2. read pull-requests permission (if private repository to obtain Pull Request Description)

if testing, use the test repository for pypi which is ``https://test.pypi.org/legacy/``, which defaults to the regular repository

```yml
on:
  pull_request:
    types: [ closed ]

jobs:
  publish:
    runs-on: ubuntu-latest
    if: github.event.pull_request.merged == true
    permissions:
      contents: write
      pull-requests: read
    steps:
      - uses: actions/checkout@v2
      - name: Bump and Publisher Distribution to PyPi
        uses: YousefEZ/auto-pypi@0.0.7
        with:
          githubtoken: ${{ secrets.GITHUB_TOKEN }}
          twinetoken: ${{ secrets.TWINE_USERNAME }}
          repository: https://test.pypi.org/legacy/

```

## 🦆 Example

You can see a sample repository that uses this Github Action [here](https://github.com/YousefEZ/auto-pypi-test)
