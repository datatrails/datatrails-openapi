
.. _bearer-token:

API Request Authorization and Authentication
--------------------------------------------

Authorization and Authentication of individual Jitsuin Archivist API requests
uses `Bearer tokens <https://tools.ietf.org/html/rfc6750#page-5>`__

See :ref:`get-api-access-token` for details on how to obtain the token. And
:ref:`config-for-non-interactive-access` for the necessary administrative configuration.

The bearer token should be stored in a file and an environment variable **BEARER_TOKEN_FILE**
contains the name of the file.

The text in the BEARER_TOKEN_FILE should follow the format:

.. code-block:: text

    Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

where the x's are replaced by the actual contents of the bearer token.

.. note::

    Recommended that the directory containing the **BEARER_TOKEN_FILE** have 0600 permissions

.. note::

   Certificate based assertion of identity is fully supported. See "client_assertion_type" and "client_assertion" in the official
   `Azure documentation <https://docs.microsoft.com/en-us/azure/active-directory/develop/v1-oauth2-client-creds-grant-flow>`__

