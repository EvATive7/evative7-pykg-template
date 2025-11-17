<div align="center">

# evative7-pykg-template

A project template for writing modern and distributable Python packages based on this, while ensuring unity of style and focus on code.

[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)

<!-- TODO: Finish this if you need badges
[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/YOURNAME/YOURREPO/package.yml)](https://github.com/YOURNAME/YOURREPO/actions)
[![Python](https://img.shields.io/pypi/pyversions/YOURPROJECT)](https://pypi.org/project/YOURPROJECT)
[![PyPI version](https://badge.fury.io/py/YOURPROJECT.svg)](https://pypi.org/project/YOURPROJECT)
[![Coverage Status](https://coveralls.io/repos/YOURNAME/YOURREPO/badge.svg?branch=develop&service=github)](https://coveralls.io/github/YOURNAME/YOURREPO?branch=master)
[![License](https://img.shields.io/github/license/YOURNAME/YOURREPO.svg)](https://pypi.org/project/YOURPROJECT/)

-->
</div>

## Quickstart

1. Generate a new project with this template
1. Set `Workflow permissions` to `Read and write permissions` on Github
1. `uv venv`
1. `source .venv/bin/activate`(bash) or `& .venv\Scripts\activate`(powershell)
1. `uv sync`
1. Finish docs, TODOs and codes

> If you need to publish to pypi...

1. Change the `if` field of `pypi-publish` Job in [package.yml](./.github/workflows/package.yml) to `true`
1. [Add a new pending publisher](https://pypi.org/manage/account/publishing/)
