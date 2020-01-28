
.. _assetv2_creation:

Asset V2 Creation
-----------------

.. include:: ../auth_url.rst


Define the asset parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
         "behaviours": ["Firmware", "Location"],
         "attributes": {
             "some": "properties",
             "location_identity": "locations/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000"
         },
         "user_mutable": ["some"]
    }

.. note::
    behaviours
        list of behaviours enabled for this asset

    attributes
        properties of asset

    user_mutable
        optional list of user-defined properties

    See :ref:`attachments_upload` and/or :ref:`locations_creation`.

    See `Swagger POST API <openapi.html#post--archivist-v2-assets>`_

Create the asset:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v2/assets


The response is:

.. code-block:: JSON

    {
        "identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f",
        "behaviours": ["Firmware", "Location"],
        "attributes": {
            "some": "properties",
            "firmware_version": "v4.9-a-beta1",
            "location_identity": "locations/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000"
        },
        "user_mutable": ["some"]
    }

.. note::
    identity
        used internally by the Jitsuin system to track this asset.

    attributes
        properties of asset

    user_mutable
        optional list of user-defined properties

    See :ref:`attachments_upload` and/or :ref:`locations_creation`.

    See `Swagger POST API <openapi.html#post--archivist-v2-assets>`_

