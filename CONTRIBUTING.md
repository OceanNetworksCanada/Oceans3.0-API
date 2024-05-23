# Set up a development environment

## Creating a virtual environment

Make sure your Python version meets the minimum version requirement defined in [sphinx](https://github.com/sphinx-doc/sphinx/blob/master/pyproject.toml#L16).
You can also check `.github/workflows/docs.yml` for the Python version used in GitHub Actions for generating the webpage.

If you are using [VS Code](https://code.visualstudio.com/docs/python/environments)
or [PyCharm](https://www.jetbrains.com/help/pycharm/creating-virtual-environment.html#python_create_virtual_env),
you can follow their website for how to create a virtual environment.

If you are using shell, run the command below

```shell
# Create a virtual environment
$ python -m venv .venv

# Activate the venv
$ source .venv/bin/activate
# For Windows, use .venv\Scripts\activate
```

## Install dependencies

```shell
$ pip install -r requirements.txt
```

## Start sphinx server

```shell
sphinx-autobuild -W docs docs/_build/html --watch "README.md"
```
