
.. _tenancies_tenancies:

Tenancy Information
-------------------

The tenancies service provides information about your Archivist tenancy.

The tenancy information includes the list of user principals who have `root` or super-user access rights.

.. include:: ../auth_url.rst

.. note::
    Only tenant `root` users are allowed to call the tenancies endpoint.  Other users will recieve a 403 response.

Fetch the current list of tenant root principals
================================================

To fetch the list of root principals, simply GET the ``tenancies/root_principals`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/tenancies/root_principals

Update the list of tenant root principals
=========================================

Define the update parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
       "root_principals": [
           {
               "issuer": "https://login.microsoftonline.com/5c129635-5858-4fe3-9bef-444f6c7ee1cf/v2.0",
               "subject": "58589bef-4fe3-9a3b-23df-8527bc45e1cf",
               "display_name": "Jane Smith",
               "email":  "jane.smith@synsation.org"
           },
           {
               "issuer": "https://login.microsoftonline.com/5c129635-5858-4fe3-9bef-444f6c7ee1cf/v2.0",
               "subject": "27bc5b4f-9a3b-4fe3-23df-e1c7bc45e1cf",
               "display_name": "Nate Rogers",
               "email":  "nate.rogers@synsation.org"
           }
        }
    }

.. note::
    issuer
        **required** The principal's issuer string for your Identity Provider.  This must match the Identity Provider for all existing root principals.

    subject
        **required** The principal's subject string as provided by your Identity Provider.

    display_name
        **optional** Friendly name for the user principal. Displayed in the Archivist GUI.

    email
        **optional** Email address for the principal.

Update the root principals by PATCHing the ``tenancies/root_principals`` resource:

.. code-block:: shell

    $ curl -v -X PATCH \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/tenancies/root_principals

.. note::
    For safety reasons you are not allowed to remove yourself from the list of root principals.
