---
$title: Install
$order: 2
$category: Get started
---
# Install Grow.dev

Grow.dev is a Python 3 program. We recommend using
[Pipenv](https://pypi.org/project/pipenv/) to manage Python installations and
versions across projects. To use Pipenv with Grow.dev, see the below steps.

Using Pipenv permits you to have a different version of Python and a different
version of Grow.dev installed on a per-project basis.

## Install Pipenv

### Mac setup

1. Install [Homebrew](https://brew.sh/).
2. Install Pipenv and LibYAML:

```bash
brew install pipenv libyaml
```

### Linux setup

1. Install [https://pypi.org/project/pipenv/](Pipenv).

## Create a Pipfile

Pipenv uses `Pipfile`s to specify Python installations and dependencies. Add a
`Pipfile` to your project root that contains the below:

```txt
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[packages]
grow = "==1.0.0"

[requires]
python_version = "3.7"
```

Once you have a Pipfile, install it using:

```bash
pipenv install
```

You can also create a Pipfile and install in one step by invoking: `pipenv
install grow`

Need to use a different version of Grow.dev? Update the versions of `grow` and
`python_version` in `Pipfile` accordingly.

## Node setup

Most Grow.dev projects rely on Node in some way for JavaScript extensions. We
recommend using `nvm` for managing Node versions.

- [Read nvm install instructions](https://github.com/nvm-sh/nvm#install-script)

Most Grow.dev extensions rely on Node versions 10x or higher.

Note for Mac users: many Node programs (i.e. popular `node-sass`) may require
Xcode and its command line tools to compile. Install Xcode using the Mac App
Store, and then follow the `xcode-select` [install
instructions](https://github.com/nodejs/node-gyp/issues/569#issue-55705963).

## Alias

For convenience, we recommend adding a global alias for `grow` to `pipenv run
grow`. This permis you to run `grow` instead of `pipenv run grow` for all
Grow commands.

```bash
# In .bash_profile (or similar).
alias grow='pipenv run grow'
```

## Using a starter

We recommend using a starter project to get started with your first Grow.dev
website. Get started with our [base starter](http://github.com/grow/starter)
which provides a `Pipfile` and a project structure that's ready to go. 

## Next steps

Once the above steps are completed, you can invoke `grow` to use the CLI. Run
the below commands from within your project directory:

```bash
# Output help.
grow --help

# Installs project dependencies (Python and Node extensions).
grow install

# Run the development server.
grow run

# Build the project.
grow build
```

Once you're familiar with the overall setup, most projects can be started with:

```
pipenv install
grow install
grow run
```

## Troubleshooting

- [LibYAML fix](/libyaml/) – Improve YAML performance

### watchdog on macOS and Python 3.8

Certain configurations of macOS and xCode may run into issues installing the
`watchdog` dependency. The simplest way to resolve this is to use Python 3.7,
which isn't impacted by the
[issue](https://github.com/gorakhargosh/watchdog/issues/689). Many systems will
have Python 3.7 available, but newer systems may only have Python 3.8.

```
# Install Python 3.7.9 globally.
brew install pyenv
pyenv install 3.7.9
pyenv global 3.7.9

# Run from your Grow project directory.
pipenv --rm
pipenv install
```

### Getting Python 3x on macOS

We recommend using the newest verson of macOS which has the newest versions of
Python 3 available. If you are on an older version of macOS, you can use
`pyenv` to install Python 3:

```
brew install pyenv
pyenv install 3.7.9
pyenv global 3.7.9
```