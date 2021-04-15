
.. _iamv1subjects_update:

IAM Subjects Update (v1)
------------------------------

.. include:: ../../auth_url.rst

Define the subjects parameters to be changed and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "wallet_pub_key": ["key1"],
        "tessera_pub_key": ["key2"]
    }

.. note::

    wallet_pub_key
        list of organisation wallet keys

    tessera_pub_key
        list of organisation tessera keys

Update the IAM Subject:

.. code-block:: shell

    $ curl -v -X PATCH \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/iam/v1/subjects/47b58286-ff0f-11e9-8f0b-362b9e155667


The response is:

.. code-block:: JSON

    {
        "identity": "subjects/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
        "wallet_pub_key": ["key1"],
        "wallet_address": ["address1"],
        "tessera_pub_key": ["key3"]
    }

.. note::

    A full API reference is available in `Swagger PATCH API <openapi.html#patch--archivist-iam-v1-identity>`_
