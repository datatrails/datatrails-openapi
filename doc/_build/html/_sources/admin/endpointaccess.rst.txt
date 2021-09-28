
.. _config-for-non-interactive-access:

Configure Client Credentials for Non-Interactive Access
-------------------------------------------------------

To enable non-interactive access to Jitsuin Archivist APIs:

#. Create an Application registration in your Azure Active Directory.
#. Grant an API access permission for the registration referring to the Jitsuin
   Archivist API
#. Create a client secret

.. note::

   Certificate based assertion of identity is fully supported. See **client_assertion_type** and **client_assertion** in the official
   `Azure documentation <https://docs.microsoft.com/en-us/azure/active-directory/develop/v1-oauth2-client-creds-grant-flow>`__

.. _application-registration:

Create an Application registration
``````````````````````````````````

* Choose any name you like.
* Account type should be: **accounts in this organisational directory only**.
* Redirect URI - leave blank.

|api-app-new-registration|
|api-app-new-registration-name-and-account-type|

.. |api-app-new-registration| image:: api-app-new-registration.png
.. |api-app-new-registration-name-and-account-type| image:: api-app-new-registration-name-and-account-type.png

The Microsoft `quickstart register app`_ guide covers the general process.

.. _`quickstart register app`: https://docs.microsoft.com/bs-latn-ba/azure/active-directory/develop/quickstart-register-app


Add an API Permission to the Application registration
`````````````````````````````````````````````````````
Your app registration must be granted access to the Jitsuin Archivist API.

|api-app-permissions-apis-my-org-uses|
|api-app-permissions-request-apis|

.. |api-app-permissions-apis-my-org-uses| image:: api-app-permissions-apis-my-org-uses.png
.. |api-app-permissions-request-apis| image:: api-app-permissions-request-apis.png


The **Application permissions** enable access to the Jitsuin Archivist API using
client secrets or certificates. The Microsoft `quickstart configure web app
access`_ guide covers the general process. For non-interactive use see
**Application permissions**.

.. _`quickstart configure web app access`: https://docs.microsoft.com/bs-latn-ba/azure/active-directory/develop/quickstart-configure-app-access-web-apis


Enable the desired Jitsuin Archivist roles
``````````````````````````````````````````
|api-app-permissions-roles|

.. |api-app-permissions-roles| image:: api-app-permissions-roles.png

Grant administrator consent for the new Application registration
````````````````````````````````````````````````````````````````
|api-app-permissions-grant-consent|
|api-app-permissions-grant-consent-success|

.. |api-app-permissions-grant-consent| image:: api-app-permissions-grant-consent.png
.. |api-app-permissions-grant-consent-success| image:: api-app-permissions-grant-consent-success.png

Add a client secret to the Application registration
```````````````````````````````````````````````````
|api-app-certificates-and-secrets-2|

.. |api-app-certificates-and-secrets-2| image:: api-app-certificates-and-secrets-2.png

Take note of the client secret and the application object id (uuid).

.. note::
   If you need to have different secrets for different Jitsuin Archivist roles
   create an application registration for each distinct set of roles.
