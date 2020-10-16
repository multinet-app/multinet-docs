SSL Configuration
=================

Since we want all data to be encrypted while it's on its way to and from users,
we use SSL encryption. There are several steps for setting up our SSL encryption,
which are documented here. The steps vary for each application, and currently,
these steps are mostly performed manually.

Since we're hosting this app over multiple domains, including the apex domain,
it was important to generate a wildcard certificate for our apps. A wildcard
domain certificate matches all subdomains of a site, and it means that we can add
an arbitrary number of apps to our subdomains without having to modify our SSL
certificates. 

Our SSL certs work for \*.multinet.app (all subdomains) and multinet.app (apex)
and are issued/verified by the Let's Encrypt CA (Certificate Authority).

Generating The Certs
--------------------

Initially, we chose to use a DNS provider without a programmatic interface, 
which caused us lots of issues. Since then, we've settled on using Cloudflare
for handling the DNS entries, which makes generating/renewing our SSL
certificates much easier. API credentials for Cloudflare exist on db.multinet.app.

Currently, we use Let's Encrypt to generate/renew our SSL certificates through
their ``certbot`` program. ``certbot`` allows us to renew our SSL certificates
automatically, and, thus, we just need to propagate those changes to the services
that use them. 

You shouldn't need to run this, but the command to set up the cert is::

    sudo certbot \
        certonly \
        --dns-cloudflare \
        --dns-cloudflare-credentials /home/ubuntu/cloudflare.ini \
        -d *.multinet.app,multinet.app \
        --preferred-challenges dns-01

Note the multiple domains specified in the ``-d`` line and the dns-01 in the
``preferred-challenges`` line. These are required for our setup and allow us to
receive a wildcard domain.

The job that updates the certificates is defined on db.multinet.app and can be
modified on the /etc/cron.d/certbot. The command is pretty simple though::

    sudo certbot renew

The cron entry just adds a random delay so that the Let's Encrypt servers don't
get crushed. 

ArangoDB Instances
------------------

There are 2 ArangoDB instance that we have to update whenever a certificate is
renewed, db.multinet.app and db-testing.multinet.app. The ArangoDB Instances
require that the the full-chain and the private key files are concatenated
together into one file. Here are the steps to combine them and update the
permissions, these should be run from db.multinet.app::

    sudo cat \
        /etc/letsencrypt/live/multinet.app/fullchain.pem \
        /etc/letsencrypt/live/multinet.app/privkey.pem \
        > /home/ubuntu/server.pem
    sudo chmod 600 /home/ubuntu/server.pem
    sudo setfacl -m u:arangodb:r /home/ubuntu/server.pem

Now you have the file updated on db.multinet.app, all that's left is to restart
the ArangoDB service with ``sudo systemctl restart arangodb3``, and to pass these
files to the other services.

The first place to send files is db-testing.multinet.app. You'll need to send the
server.pem file using ``magic-wormhole``. To send the files follow these steps::
    
    # On db.multinet.app
    wormhole send /home/ubuntu/server.pem

    # On db-testing.multinet.app
    cd /home/ubuntu
    mv server.pem server.pem.old
    wormhole receive <token>
    sudo chmod 600 /home/ubuntu/server.pem
    sudo setfacl -m u:arangodb:r /home/ubuntu/server.pem
    sudo systemctl restart arangodb3


Netlify
-------

We currently have 3 client apps that must be updated when a certificate is
renewed: multinet.app, nodelink.multinet.app, and adjmatrix.multinet.app.

First you need to add a custom domain. You can do this by clicking on the app,
then clicking "Domain Settings" near the top. After that, you should see a
section near the top that says "Custom Domains" with a button that says 
"Add custom domain". Click that button, add the desired domain, and click 
"Verify". It'll warn you about it not being registered through netlify,but just
click "Yes, add domain". 

Once that’s done, scroll down to the "HTTPS" section, there should be a button
along the lines of "Supply custom certificate", **NOT** the "Use Let’s Encrypt
certificate" button. There it will ask you for the certificate, private key,
and intermediate certs, which should be supplied in the following manner:

    :Certificate: cert.pem
    :Private Key: privkey.pem
    :Intermediate Certs: fullchain.pem

You’ll have to do this by just copying and pasting the text of those files into
their respective fields. Once that’s done, click "Install Certificate". After
this, there should be a warning about not enforcing HTTPS, I recommend clicking
the "Force HTTPS" button to have HTTP requests automatically forward to HTTPS.
That’s it for Netlify.

Another note, once the custom certificate is supplied for one of the
applications, it will probably show up automatically for the others as well,
so you may be able to skip this step after doing it once.


Heroku
------

Finally, we must also update our Heroku deployment, api.multinet.app, to use the
new SSL certificates. 

Making these changes on heroku isn’t quite as simple initially thought, because,
you can’t just point the DNS record to https://multinet-app.herokuapp.com. 
Instead, you need to set a custom domain in the "Domains" section of the settings.

Once you’ve done that, you need to supply the DNS Target specified above to your
DNS Provider (in our case Cloudflare), as the target to resolve to. Once you’ve done
that, you can add the certificate in the "SSL Certificates" section of the
settings. You can do that by clicking the "Configure SSL" button, then "Manual
Certificate". When it asks for the public certificate, you should supply the
"fullchain.pem" file, and when it asks for the private key, supply the
"privkey.pem" file.

That’s it for heroku. However, it might take a while for your browser to update
(I ran into this issue). I’d recommend testing it on another browser, or in an
incognito session or something.

----

**Known Problems**

- We no longer receive updates about our SSL certs being renewed, since the
  renewals happen before they would expire. This means that Let's Encrypt thinks
  that the certs have been refreshed and will be used automatically, but they
  require this manual update process from above.

- Heroku certs may persist in the browser cache. To test that the cert is
  deployed, we recommend testing it on another browser, or in an incognito session.


