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

- Docker
- Python 3.7
- Pipenv
- Node
- Yarn

Build and Run ``multinet-server``
---------------------------------

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-server``.
2. Move into the repository: ``cd multinet-server``.
3. Copy the ``.env.default`` file: ``cp .env.default .env`` (or symlink it: ``ln
   -s .env.default .env``).
4. Install the Python dependencies: ``pipenv install``.
5. Run the server application in dev mode: ``pipenv run serve``.
6. Point your web browser to http://localhost:5000 to ensure that the server is
   working.

Launch ArangoDB
---------------

1. Move into the server repository's ``devops`` directory: ``cd
   multinet-server/devops``.
2. Run the docker container for ArangoDB: ``docker-compose up``.

Build and Run ``multinet-client``
---------------------------------

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-client``.
2. Move into the repository: ``cd multinet-client``.
3. Install the project dependencies: ``yarn install``.
4. Serve the application in dev mode: ``yarn serve``.
5. Point your web browser to http://localhost:8080 to see the client running.

At this point, you should have a working development build of Multinet. See the
rest of this documentation for details on how Multinet works, and how to develop
with Multinet. If you have questions, contact us at multinet@kitware.com, or
file a report on the `issue tracker
<https://github.com/multinet-app/multinet-client/issues>`_.
