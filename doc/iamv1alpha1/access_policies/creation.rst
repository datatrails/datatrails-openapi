
.. _iamv1alpha1access_policies_creation:

IAM Access Policies Creation (v1alpha1)
---------------------------------------

.. include:: ../../auth_url.rst

Define the access_policies parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Some description",
        "filters": "[
            [\"location=basingstoke\", \"location=cambridge\"],
            [\"asset_type=door_access_reader\"]
        ]",
        "access_permissions": [
            {
                "access_keys": [
                    {
                        "tessera": [ "key1", "key2" ],
                        "wallet": [ "key3", "key4" ]
                    },
                    {
                        "tessera": [ "key5", "key6" ],
                        "wallet": [ "key7", "key8" ]
                    }
                ],
                "behaviours": [ "behaviour1", "behaviour2" ],
                "include_attributes": [ "attribute1", "attribute2" ]
            }
        ]
    }

.. note::
    display_name
        **required** Friendly name for the location. Displayed in the Archivist GUI.

    filters
        String containing JSON of list of listes of selectors

    access_permissions
        access_keys
            list of maps of wallet and tessera keys

        behaviours
            list of behaviours

        include_attributes
            list of included attributes

Create the access policy:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1alpha1/iam/access_policies


The response is:

.. code-block:: JSON

    {
        "identity": "access_policies/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
        "filters": "[
            [\"location=basingstoke\", \"location=cambridge\"],
            [\"asset_type=door_access_reader\"]
        ]",
        "access_permissions": [
            {
                "access_keys": [
                    {
                        "tessera": [ "key1", "key2" ],
                        "wallet": [ "key3", "key4" ]
                    },
                    {
                        "tessera": [ "key5", "key6" ],
                        "wallet": [ "key7", "key8" ]
                    }
                ],
                "behaviours": [ "behaviour1", "behaviour2" ],
                "include_attributes": [ "attribute1", "attribute2" ]
            }
        ]
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v1alpha1-iam-access_policies>`_
