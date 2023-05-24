.. _OAuth2 Credentials:

OAuth2 Credentials
==================

Multinet uses Google's OAuth2 to verify the identity of users accessing the
client.

Google OAuth2 Steps
-------------------------------

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
