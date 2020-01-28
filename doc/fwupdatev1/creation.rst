
.. _fwupdatev1v2_creation:

Firmware Update Creation
------------------------

.. include:: ../auth_url.rst


Define the event parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
      "operation": "Update",
      "behaviour": "FwUpdateV1",
      "attributes": {
          "firmware_version": "3.2.1",
      },
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "principal_declared": {
        "issuer": "job.idp.server/1234",
        "subject": "bob@job"
      }
    }

.. note::
    attributes
        properties of asset

    timestamp_declared
        Time at which update was preformed

    principal_declared
        Identity of person who did the update

    See `Swagger POST API <openapi.html#post--archivist-v2-fwupdatev1>`_

Create the firmware update:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v2/assets/add30235-1424-4fda-840a-d5ef82c4c96f/events


The response is:

.. code-block:: JSON

    {
      "identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f/events/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
      "asset_identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f",
      "operation": "Update",
      "behaviour": "FwUpdateV1",
      "attributes": {
          "firmware_version": "3.2.1",
      },
      "timestamp_accepted": "2019-11-27T14:44:19Z",
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "timestamp_committed": "2019-11-27T14:44:19Z",
      "principal_declared": {
        "issuer": "job.idp.server/1234",
        "subject": "bob@job"
      },
      "principal_accepted": {
        "issuer": "job.idp.server/1234",
        "subject": "bob@job"
      },
      "confirmation_status": "CONFIRMED",
      "block_number": 12,
      "transaction_index": 5,
      "transaction_id": "0x07569"
    }

.. note::
    identity
        used internally by the Jitsuin system to track this event.

    asset_identity
        identity of asset (uuid)

    attributes
        properties of asset

    timestamp_accepted
        Time at which update was preformed

    timestamp_committed
        Time at which update was preformed

    timestamp_declared
        Time at which update was preformed

    principal_declared
        Identity of person who did the update

    principal_accepted
        Identity of person who did the update

    confirmation_status
        CONFIRMED is committed to blockchain

    block_number transaction_index transaction_id
        Details of event on blockchain

    See `Swagger POST API <openapi.html#post--archivist-v2-fwupdatev1>`_

