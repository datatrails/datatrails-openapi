
.. _asset_creation:

Asset Creation
--------------

.. include:: ../auth_url.rst


Define the asset parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "type": "SimpleDeviceAsset",
        "display_name": "mydevice",
        "location_identity": "location/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
        "extended_attributes": {
            "some": "properties"
        },
        "type_attributes": {
            "firmware_version": "v45.6",
            "serial_number": "f867662g.1"
        },
        "attachments": [
            {
                "attachment_identity": "attachments/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
                "display_name": "primary_image"
            },
            {
                "attachment_identity": "attachments/11bf5b37-42e0-42e0-8dcf-dc8c4aefc000",
                "display_name": "form B7"
            }
        ]
    }


.. note::
    The fields **location_identity** and **attachments** are optional.

    See :ref:`attachments_upload` and/or :ref:`locations_creation`.

    The **"type"** field is **required** and must equal 'SimpleDeviceAsset'.

    The **"display_name"** field is **required**.

    See `Swagger POST API <openapi.html#post--archivist-v1-assets>`_

Create the asset:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/assets


The response is:

.. code-block:: JSON

    {
        "identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f",
        "type": "SimpleDeviceAsset",
        "display_name": "mydevice",
        "description": "my favourite asset",
        "confirmation_status": "CONFIRMATION_STATUS_CONFIRMED",
        "tracked": "TRACKED",
        "location_identity": "locations/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
        "extended_attributes": {
            "some": "properties"
        },
        "type_attributes": {
            "firmware_version": "v45.6",
            "serial_number": "f867662g.1"
        },
        "attachments": [
            {
                "attachment_identity": "attachments/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
                "display_name": "primary_image"
            },
            {
                "attachment_identity": "attachments/add30235-1424-4fda-840a-d5ef82c4c96f",
                "display_name": "form B7"
            }
        ]
    }

.. note::
    The **"identity"** field is used internally by the Jitsuin system to track this asset.

    The additional field **"confirmation_status"** can have 2 values:

        1. "CONFIRMATION_STATUS_PENDING": asset has not yet been registered on the Ledger.
        2. "CONFIRMATION_STATUS_CONFIRMED": asset has been registered on the Ledger.

