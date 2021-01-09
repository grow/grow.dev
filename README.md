grow.dev
===========
[![Circle CI](https://circleci.com/gh/grow/grow.io.png?style=shield)](https://circleci.com/gh/grow/grow.io)

The documentation website for [Grow.dev](https://github.com/grow/grow).

## Developer setup

This project uses [Grow.dev](https://grow.dev), a static site generator.

### Prerequisites

At a minimum, you will need:

- [Pipenv](https://pipenv.pypa.io/en/latest/install/#installing-pipenv)
- [Node](https://github.com/nvm-sh/nvm#installing-and-updating)

After Pipenv and Node are setup, install the project using the following
command. This installs the correct version of Python, and also installs Grow.

### Install, alias, and run

```bash
# Run from the project directory.
pipenv install

# Add an alias to `$HOME/.bashrc` for grow.
alias grow='pipenv run grow'

# Init a grow project with the base theme in the current directory.
# Feel free to use any other theme than base from https://github.com/growthemes.
grow init base ./

# Install project dependencies.
grow install

# Run the development server
grow run
```

## Deployment

`grow.dev` is hosted on Google Cloud Storage. Commits on GitHub's `master`
invoke a Circle CI build task that automatically deploy the changes.
