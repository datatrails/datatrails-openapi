
.. _asset_firmware:

Asset Update Firmware Event
---------------------------

.. include:: ../auth_url.rst

Define the asset_identity:

.. code-block:: shell

    $ ASSET_IDENTITY=assets/add30235-1424-4fda-840a-d5ef82c4c96f

Define the firmware update event(s) and store in /path/to/jsonfile:

.. code-block:: JSON

    [
        {
            "asset_identity": "$ASSET_IDENTITY",
            "type": "AttributeUpdate",
            "extended_attributes": {
              "what": "did something!"
            },
            "type_attributes": {
              "field": "type_attributes.firmware_version",
              "value": "v45.7"
            },
            "principal_declared": {
              "issuer": "job.idp.server/1234",
              "subject": "bob@job"
            },
            "description": "Did something",
            "attachments": []
        }
    ]

.. note::
    attachments
        optional.

    See :ref:`attachments_upload`.

    asset_identity
        **required** in each instance.

    More than one event can be registered in the same POST request.

    For example one can specify additional maintenance and other events

    See :ref:`asset_maintenance`.

    See `Swagger POST API <openapi.html#post--archivist-v1-asset_identity-events>`_


Register the events on different assets:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/assets/$ASSET_IDENTITY/events


The response is:

.. code-block:: JSON

    [
        {
            "identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f/events/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
            "asset_identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f",
            "principal_declared": {
                "issuer": "job.idp.server/1234",
                "subject": "bob@job"
            },
            "principal_accepted": {
                "issuer": "job.idp.server/1234",
                "subject": "bob@job"
            },
            "description": "Did something",
            "timestamp_declared": "2019-11-07T15:31:40Z",
            "confirmation_status": "CONFIRMATION_STATUS_CONFIRMED",
            "timestamp_committed": "2019-11-07T15:31:49Z",
            "timestamp_accepted": "2019-11-07T15:31:45Z",
            "extended_attributes": {
                "patch": "af445dde7"
            },
            "type": "AttributeUpdate",
            "transaction_id": "0x04756",
            "block_number": 12,
            "transaction_index": 5,
            "type_attributes": {
                "field": "type_attributes.firmware_version",
                "value": "v45.7"
            }
        }
    ]


.. note::
    identity
        used internally by the Jitsuin system to track this event.

    confirmation_status
        1. "CONFIRMATION_STATUS_PENDING": asset has not yet been registered on the Ledger.
        2. "CONFIRMATION_STATUS_CONFIRMED": asset has been registered on the Ledger.

