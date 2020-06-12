grow.io  [![Circle CI](https://circleci.com/gh/grow/grow.io.png?style=shield)](https://circleci.com/gh/grow/grow.io)
===========

Grow's open source project page and documentation.

## Contributing

    # Install Grow.
    curl https://install.grow.io | bash

    # Clone the repo.
    git clone https://github.com/grow/grow.io.git

    # Run the preview server.
    grow run grow.io

## Deployment

`grow.io` is hosted on Google Cloud Storage. Commits on GitHub kick off a Circle CI build task that automatically deploy the changes.

## Python 2 Deprecation

Python 2 has reached the end of life for support. Grow is in the process of moving from pythong 2 to python 3.
