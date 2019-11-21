
.. _asset_maintenance:

Asset Maintenance Event
-----------------------

.. include:: ../auth_url.rst

Define the asset_identity:

.. code-block:: shell

    $ ASSET_IDENTITY=assets/add30235-1424-4fda-840a-d5ef82c4c96f

Define the maintenance event(s) and store in /path/to/jsonfile:

.. code-block:: JSON

    [
        {
            "asset_identity": "$ASSET_IDENTITY",
            "type": "Maintenance",
            "extended_attributes": {
                "what": "did something!"
            },
            "type_attributes": {},
            "principal_declared": {
                "issuer": "job.idp.server/1234",
                "subject": "bob@job"
             },
             "description": "Did something",
             "attachments": [
                  {
                      "attachment_identity": "attachments/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
                      "display_name": "form B5"
                  },
                  {
                      "attachment_identity": "attachments/add30235-1424-4fda-840a-d5ef82c4c96f",
                      "display_name": "Maintanance Report"
                  }
             ]
         }
     ]

.. note::
    attachments
        optional.

    See :ref:`attachments_upload`.

    asset_identity
        **required** in each instance.

    More than one event can be registered in the same POST request.

    For example one can specify additional firmware and other events

    See :ref:`asset_firmware`.

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
                "issuer": "",
                "subject": "Bob from Suffolk"
            },
            "principal_accepted": {
                "issuer": "job.idp.server/1234",
                "subject": "bob@job"
            },
            "description": "Did something",
            "timestamp_declared": "2019-11-07T15:31:49Z",
            "confirmation_status": "CONFIRMATION_STATUS_CONFIRMED",
            "timestamp_committed": "2019-11-07T15:31:49Z",
            "timestamp_accepted": "2019-11-07T15:31:49Z",
            "extended_attributes": {
                "action": "checked it"
            },
            "type": "Maintenance",
            "transaction_id": "0x04756",
            "block_number": 12,
            "transaction_index": 5,
            "type_attributes": {},
            "attachments": [
                {
                    "attachment_identity": "attachments/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
                    "display_name": "form B5"
                },
                {
                    "attachment_identity": "attachments/add30235-1424-4fda-840a-d5ef82c4c96f",
                  "display_name": "form B7"
                }
            ]
        }
    ]


.. note::
    identity
        used internally by the Jitsuin system to track this event.

    confirmation_status
        1. "CONFIRMATION_STATUS_PENDING": asset has not yet been registered on the Ledger.
        2. "CONFIRMATION_STATUS_CONFIRMED": asset has been registered on the Ledger.

