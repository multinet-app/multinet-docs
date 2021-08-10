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
- Python 3.7 and Pip
  (`Windows <https://docs.python-guide.org/starting/install3/win/#install3-windows>`_,
  `MacOS <https://docs.python-guide.org/starting/install3/osx/#install3-osx>`_,
  `Ubuntu <https://docs.python-guide.org/starting/install3/linux/#install3-linux>`_)
- Pipenv
  (`Windows <https://pipenv.pypa.io/en/latest/install/#pragmatic-installation-of-pipenv>`_,
  `MacOS <https://pipenv.pypa.io/en/latest/install/#homebrew-installation-of-pipenv>`_,
  `Linux <https://pipenv.pypa.io/en/latest/install/#pragmatic-installation-of-pipenv>`_)
- Node
  (`All OSes <https://docs.npmjs.com/downloading-and-installing-node-js-and-npm>`_)
- Yarn
  (`Windows <https://classic.yarnpkg.com/en/docs/install/#windows-stable>`_,
  `MacOS <https://classic.yarnpkg.com/en/docs/install/#mac-stable>`_,
  `Linux <https://classic.yarnpkg.com/en/docs/install/>`_)

Launch ArangoDB
---------------

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-server``.
2. Move into the server repository: ``cd multinet-server``.
3. Run the docker container for ArangoDB: ``docker-compose up``. (On Macs, you
   may need to use an alternate command: ``ARANGO_DATA=~/.local/multinet/arango
   docker-compose up``.) If you're getting an error that looks like ``docker-compose: 
   command not found``, make sure that the docker application is running.
4. When the container is running, you'll need to make a new user on ArangoDB. To do so,
   navigate to http://localhost:8529 and log in with the default username and password,
   "root" and "letmein", respectively.
5. Now that you're logged in, navigate to the "_system" database and then to "users" on
   the left panel in the dashboard.
6. Click "Add User" setting username to "readonly" and password to "letmein". Click
   create to make the user.
7. Now click on the user readonly to set its permissions. After clicking readonly, click
   "permissions". On the permissions page, on the line that starts with "*", click the radio
   button that corresponds to access. At this point click on "dashboard" to complete the
   setup.

**NOTE**: if you're deploying in production, make sure you update the user passwords in
ArangoDB and in the .env in multinet-server

Build and Run ``multinet-server``
---------------------------------

1. Move into the repository: ``cd multinet-server``.
2. Copy the ``.env.default`` file: ``cp .env.default .env`` (or symlink it: ``ln
   -s .env.default .env``).
3. Create :ref:`OAuth2 Credentials` and make sure to copy them to your .env file.
4. Install the Python dependencies: ``pipenv install``.
5. Run the server application in dev mode: ``pipenv run serve``.
6. Point your web browser to http://localhost:5000 to ensure that the server is
   working.

Build and Run ``multinet-client``
---------------------------------

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-client``.
2. Move into the repository: ``cd multinet-client``.
3. Install the project dependencies: ``yarn install``.
4. Set up the appregistry: ``yarn init-appregistry``.
5. Serve the application in dev mode: ``yarn serve``.
6. Point your web browser to http://localhost:8080 to see the client running.

At this point, you should have a working development build of Multinet. See the
rest of this documentation for details on how Multinet works, and how to develop
with Multinet. If you have questions, contact us at multinet@kitware.com, or
file a report on the `issue tracker
<https://github.com/multinet-app/multinet-client/issues>`_.
