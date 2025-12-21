<div align="center">

# evative7-pykg-template

A project template for writing modern and distributable Python packages based on this, while ensuring unity of style and focus on code.

[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)

<!-- TODO: Finish this if you need badges
Replace: `YOURPROJECT`, `YOURNAME`, `YOURREPO`

[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/YOURNAME/YOURREPO/package.yml)](https://github.com/YOURNAME/YOURREPO/actions)
[![Python](https://img.shields.io/pypi/pyversions/YOURPROJECT)](https://pypi.org/project/YOURPROJECT)
[![PyPI version](https://badge.fury.io/py/YOURPROJECT.svg)](https://pypi.org/project/YOURPROJECT)
[![Coverage Status](https://coveralls.io/repos/YOURNAME/YOURREPO/badge.svg?branch=develop&service=github)](https://coveralls.io/github/YOURNAME/YOURREPO?branch=master)
[![License](https://img.shields.io/github/license/YOURNAME/YOURREPO.svg)](https://pypi.org/project/YOURPROJECT/)

-->
</div>

<!-- TODO: Remove below -->

## Quickstart

1. Generate a new project with this template
1. Set `Workflow permissions` to `Read and write permissions` on Github
1. Set `Allow GitHub Actions to create and approve pull requests` on Github
1. Finish `pyproject.toml`
1. `uv sync --all-extras`
1. Finish docs, LICENSE, TODOs and codes
1. Follow the **Conventional Commit** rules strictly when writing commit messages.
   `release-please` will automatically manage version updates and releases based on **SemVer**.
   To manually specify a version, add `Release-As: x.x.x` in the commit body.

> If you need to publish to pypi...

1. Change the `if` field of `pypi-publish` Job in [package.yml](./.github/workflows/package.yml) to `true`
1. [Add a new pending publisher](https://pypi.org/manage/account/publishing/)

## Migration guide (v0.0.3 → v0.0.4)

### `.github/workflows/package.yml`

```diff
@@ x @@ jobs:
         run: uv sync

       - name: Build distributions
+        env:
+          SETUPTOOLS_SCM_PRETEND_VERSION: ${{ needs.release-please.outputs.tag_name }}
         run: uv build

       - name: Upload distributions
@@ x @@ jobs:
       contents: read
       id-token: write

-    environment:
-      name: release
-
     steps:
       - name: Retrieve release distributions
         uses: actions/download-artifact@v4
```

### `.pyproject.toml`

```diff
@@ x @@
 [build-system]
-build-backend = "setuptools.build_meta"
-requires = ["setuptools-scm"]
+requires = ["hatchling", "hatch-vcs"]
+build-backend = "hatchling.build"

@@ x @@
-[tool.setuptools.package-dir]
-"" = "src"
-
-[tool.setuptools_scm]
-version_scheme = "post-release"
-local_scheme = "node-and-date"
+[tool.hatch.build.targets.sdist]
+exclude = [
+  "/.github",
+  "/.vscode",
+  "/uv.lock",
+  "/.gitignore",
+]

+[tool.hatch.version]
+source = "vcs"

 # TODO: Finish this file if you need to add anything
```

## Migration guide (v0.0.2 → v0.0.3)

- **`.flake8`, `.pre-commit-config.yaml`** — removed

- **`.gitignore`**

  ```diff
  -CHANGELOG.md
  ```

- **`CHANGELOG.md`** — added (blank)

- **`README.md`**

  ```diff
  +[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
  ```

- **`pyproject.toml`**

  - Python version
  - Config & dependencies

    ```diff
    -requires = ["setuptools", "wheel", "setuptools-scm"]
    +requires = ["setuptools-scm"]

    -build = ["build"]
    -dev = ["black", "isort", "flake8", "pytest", "pre-commit"]
    +dev = ["ruff", "pytest"]

    -[tool.isort]
    -profile = "black"
    ```

- **`.github/workflows/package.yml`** — updated

  - Check `if` option of `pypi-publish` Job

- Others

  - Set `Allow GitHub Actions to create and approve pull requests` on Github
  - `pre-commit uninstall`
  - Quickstart:

    ```diff
    -1. `python -m venv .venv`
    -1. `pip install .[dev,build]`
    -1. `pre-commit install`
    +1. `uv sync --all-extras`
    ```
