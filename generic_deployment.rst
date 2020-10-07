Deploying On Any Platform
=========================

To deploy Multinet on a platform other than Heroku, there are some generic
steps that you can take. We offer these steps as a simple guide that will likely
require some refinement for your specific deployment.

We follow the 12 factor app paradigm as described `here <https://12factor.net/>`_.
This should also inform your deployment strategy, and we recommend deploying each
program of our stack on separate servers. There are also some tips for a
monolithic deployment below, just in case that is your only option.

ArangoDB
--------

Your ArangoDB instance should be installed to your server/vm and initialized with
a **strong** ``root`` password. You're welcome to change the port here if that
satisfies your security concerns. 

Once you've set up your root user, connect to the ArangoDB instance using the
default port (or the port you set), and create a user called ``readonly``. This
user should also have a strong password, but the risk here is slightly lower.
Once you've set this user up, you should go to their permissions and set
read-write access to all databases by clicking access for the database ``*``.

There may also be some additional configuration that you'll need to in order
for the ``multinet-server`` instance to communicate with the database. This
might include port forwarding and establishing firewall rules, but will differ
on a case-by-case basis.

``multinet-server``
-------------------

Make sure you have python3.7 and pipenv installed. Then:

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-server``.
2. Move into the repository: ``cd multinet-server``.
3. Copy the ``.env.default`` file: ``cp .env.default .env`` (or symlink it: ``ln
   -s .env.default .env``).
4. Create :ref:`OAuth2 Credentials` and make sure to copy them to your .env file.
5. Set ALLOWED_ORIGINS to the address for your ``multinet-client`` instance,
   including the method (e.g. https://multinet.app, yours will be different)
6. Set your ARANGO_PASSWORD to the ``root`` password for ArangoDB, and your 
   ARANGO_READONLY_PASSWORD to the password you created for the ``readonly`` user.
7. Install the Python dependencies: ``pipenv install``.
8. Run the server application in production mode with:
   ``pipenv run gunicorn multinet.app:app``. **NOTE:** This uses gunicorn's
   default settings, where the app is hosted on http://127.0.0.1:8000. There are
   cases where a socket would be best (e.g. when using reverse proxies, see 
   `below <#using-reverse-proxies>`_). In that case, run the same command with
   an additional flag, for example: ``pipenv run gunicorn --bind unix:./socket.sock multinet.app:app``.
   The socket will be located in the ``multinet-server`` directory.

``multinet-client``
-------------------

1. Clone the repository: ``git clone https://github.com/multinet-app/multinet-client``.
2. Move into the repository: ``cd multinet-client``.
3. Install the project dependencies: ``yarn install``.
4. Build the production app: ``yarn build``.

At this point, you have a few options for how to proceed. The most recommended
way to continue is to serve these files using a production webserver such as
`nginx <https://www.nginx.com/>`_ or `apache webserver <https://httpd.apache.org/>`_.
See the docs for these projects for details on how to do that.

Handling DNS
------------

Since all of these services should be deployed onto separate servers/vms the
easiest way to handle accessing them is through DNS. If you have a domain, you
can set subdomains for each program in the stack. For example:

* db for the ArangoDB instance
* api for the ``multinet-server`` application
* @ and www for the ``multinet-client`` application

There may be some additional apps that you can host on the same domain. For
example, we host MultiLink and MultiMatrix on subdomains of our main domain.

Using Reverse Proxies
---------------------

If you do decide to deploy these on a monolithic server, with all the apps
together, you can't use the DNS method from above. Instead, you'll have to run
a reverse proxy using a program such as `nginx <https://www.nginx.com/>`_,
or `apache webserver <https://httpd.apache.org/>`_.

Here's an example of an nginx.conf file that you might use::

   TODO: config goes here

