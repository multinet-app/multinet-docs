.. _developer_quick_start:

Developer Docs
==============

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
  (`Windows <https://classic.yarnpkg.com/en/docs/install/#windows-stable>`__,
  `MacOS <https://classic.yarnpkg.com/en/docs/install/#mac-stable>`__,
  `Linux <https://classic.yarnpkg.com/en/docs/install/>`_)

Install and Launch the applications
-----------------------------------

The most up to date instructions for installing and launching the applications is in the `README.md` file in each repository. The best order of operations for getting the infrastructure running is to start with the API, then the client, then the visualization apps. To get everything set up:

1. Clone the repositories for the API, client, and visualization apps.
2. Follow the instructions in the `README.md` file in `multinet-api <https://github.com/multinet-app/multinet-api>`_ to launch the databases and the API server.
3. Follow the instructions in the `README.md` file in `multinet-client <https://github.com/multinet-app/multinet-client>`_ to launch the client.
4. Follow the instructions in the `README.md` file in the each of the three visualization apps (`MultiLink <https://github.com/multinet-app/multilink>`_, `MultiMatrix <https://github.com/multinet-app/multimatrix>`_, and `UpSet <https://github.com/visdesignlab/upset2>`_) to launch the visualization apps.

OAuth2 Credentials
------------------

Multinet uses Google's OAuth2 to verify the identity of users accessing the
client.

If you're a developer on the main Multinet project (i.e. the one hosted on
multinet.app), you can request our production credentials from an administrator.

Otherwise, to enable OAuth2 on your own project, you'll have to:

1. Either have or `create <https://console.developers.google.com/projectcreate>`_ 
   a Google Cloud project.
2. Navigate to the `OAuth consent screen section <https://console.developers.google.com/apis/credentials/consent>`_.
3. Configure your consent screen, and select "Internal" or "External" based on
   your application requirements ("External" is usually correct if the
   instance will be public-facing). Multinet requires the "email", "profile',
   and 'openid' scopes to run correctly. **NOTE:** Adding a logo means your
   app will have to go through verification, which can take 6 weeks.
4. Now go to the `"credential" section <https://console.developers.google.com/apis/credentials>`_,
   and select "Create Credentials" > "OAuth client ID". 
5. Set Application type to "Web application" and set a redirect URI. By default,
   multinet uses <baseurl>/api/user/oauth/google/authorized (note that <baseurl> is usually http://localhost:8000)
6. Copy the resulting client ID and secret key into your `multinet-server` .env file as `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`.
