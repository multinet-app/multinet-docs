.. _quickstart:

Quick Start
===========

The easiest way to get started with Multinet is to go to https://multinet.app,
and begin experimenting.

To build a local development environment, you will need to *install
dependencies*, *launch a database*, *build and run the server*, and *build and
run the client*.  Follow these steps:

Install Dependencies
--------------------

These projects are built using the following tools; ensure that you have them
installed:

- Docker and Docker Compose
  (`Windows <https://docs.docker.com/docker-for-windows/install/>`_,
  `MacOS <https://docs.docker.com/docker-for-mac/install/>`_,
  `Linux Docker Engine <https://docs.docker.com/engine/install/>`_,
  `Linux Docker Compose <https://docs.docker.com/compose/install/#install-compose>`_)
- Node
  (`All OSes <https://docs.npmjs.com/downloading-and-installing-node-js-and-npm>`_)
- Yarn
  (`Windows <https://classic.yarnpkg.com/en/docs/install/#windows-stable>`_,
  `MacOS <https://classic.yarnpkg.com/en/docs/install/#mac-stable>`_,
  `Linux <https://classic.yarnpkg.com/en/docs/install/>`_)

Install and Launch the applications
-----------------------------------

The most up to date instructions for installing and launching the applications is in the `README.md` file in each repository. The best order of operations for getting the infrastructure running is to start with the API, then the client, then the visualization apps. To get everything set up:

1. Clone the repositories for the API, client, and visualization apps.
2. Follow the instructions in the `README.md` file in `multinet-api <https://github.com/multinet-app/multinet-api>`_ to launch the databases and the API server.
3. Follow the instructions in the `README.md` file in `multinet-client <https://github.com/multinet-app/multinet-client>`_ to launch the client.
4. Follow the instructions in the `README.md` file in the each of the three visualization apps (`MultiLink <https://github.com/multinet-app/multilink>`_, `MultiMatrix <https://github.com/multinet-app/multimatrix>`_, and `UpSet <https://github.com/visdesignlab/upset2>`_) to launch the visualization apps.

