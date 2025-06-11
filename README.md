# Project-Management
This repo describes and explains how we manage and configure all our python bots.
All Disutils bot developers are required to brief this repo and if you are one reading this, make sure you have python version `3.12.x` installed in your system.

## Introduction

We use the `uv` project manager for our bots. `uv` handles configuration, dependencies and environments while being extremely fast and efficient!

To get started with it you first need to install it in your system.
You can download `uv` through `pip`, `cargo`, `homebrew`, `winget` or even `scoop`.

Through pip, run the following command–

```
pip install uv
```

and make sure you're running this command in your **Global Environment**.
If you want to use some other package manager, you can look up the installation docs [here](https://docs.astral.sh/uv/getting-started/installation/#installing-uv).

If you have `pip` set to PATH you can invoke `uv` directly. If you cannot use `uv` directly you can invoke it via–

* `py -m uv` for Windows.
* `python3 -m uv` for Unix / macOS.

## Getting Started

After you've done installing `uv` into your system, you need to configure all its dependencies and environment in your local system.

### Configuring an existing uv project

Since all our bots already have the required meta files, configuring it in our system is pretty easy and straightforward.
Once you have `git clone`'ed the repo you want, run the following command in your terminal–

```
uv sync
```

This will sync the metadata of the files to your entire virtual environment which is created automatically and also download all dependencies.

### Creating and configuring a uv project

If you want to configure `uv` for a project, you can do so by running the following command–

```
uv init project-title-name
```

If you have already created a project and / or working on one, you can run this command instead–

```
uv init --directory "."
```

This sets the currently opened directory as a uv project.

Once this is done, uv will add the following files to your project–

* `pyproject.toml` - Contains all metadata.
* `.python-version` - The Python version `uv` should use.
* `uv.lock` - The lockfile for dependencies.

In short, you don't need to worry about these files and in most cases you don't need to modify them manually.

## Adding a dependency

To add a dependency to your project it's as easy as–

```
uv add package_name
```

When you're adding dev dependencies make sure to add the `--dev` flag like so: `uv add package_name --dev`.
Dev dependencies are those which are only required for local work and serve no purpose in production such as `ruff`, `isort`, `basedpyright`, etc.

## Removing a dependency

```
uv remove package_name
```

## Exporting

Since the host isn't capable of using `uv`, we have to manually export our dependencies to a `requirements.txt` file.
We can do this by–

```
uv export > requirements.txt --no-dev
```

This extracts all dependencies which are not a part of the `dev` group and places it in the `requirements.txt` file.
You will also notice that the requirements file contains more than just library names.
The extra data you will find in the file is a bunch of hashes of the library to maintain file integrity which adds a layer of security.

## Running files / tools

If you're using VSCode or PyCharm, they should handle the activation of the venv automatically so you can run your files like how you used to.
But in case you are not using any IDEs, you can run your files via–

```
uv run filename.py
```

In most cases you would be able to invoke any downloaded tools directly but in case you aren't able to you can use `uv run toolname` to invoke it.

## Extras

* `uv tree` : Shows a dependency tree of your project.
* `uv python` : Manage your Python version via uv.
* `uv lock` : Updates the lock file.
* `uv pip` : Manually invoke pip via uv.
