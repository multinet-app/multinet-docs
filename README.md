# multinet-docs

This repository contains the source code for the Multinet project documentation.
Read the live documentation at [Read The
Docs](https://multinet-app.readthedocs.io), visit the [Multinet project
page](https://vdl.sci.utah.edu/projects/2019-nsf-multinet), or try the [Multinet
app](https://multinet.app) to learn more about the project.

## Quick Start

You can read the current version of the documentation at
https://multinet-app.readthedocs.io. To build your own local version, follow
these steps:

1. Be sure that Pipenv is installed on your system.
2. Check out this repository, then move into it (e.g., `cd multinet-docs`).
3. Make a live copy of the environment file: `cp .env.default .env` (or, if you
   prefer, use a symlink: `ln -s .env.default .env`).
4. Install the project dependencies: `pipenv install`.
5. Build and serve the documentation: `pipenv run autobuild`.
6. Point your web browser to http://localhost:8000 to see the documentation.
