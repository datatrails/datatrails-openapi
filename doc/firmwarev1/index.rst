
.. include:: ../auth_url.rst

.. _firmware_behaviour:

Firmware Operations API
-------------------------------------------------------------------------------

.. _firmware_behaviour_Update:

Firmware Update
...............................................................................

Define the event parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
      "operation": "Update",
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "Patched during regular patch window",
        "arc_firmware_version": "3.2.1",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
      }
    }

.. note::
    attributes.arc_description
        *Required* Details of the Firmware request

    attributes.arc_firmware_version
        *Required* New firmware version

    attributes.arc_correlation_value   
        *Optional* Used to link related events together

    timestamp_declared
        *Optional* Client-claimed time at which the maintenance was performed

    principal_declared
        *Optional* Client-claimed identity of person performing the operation

Add the Firmware request to the Asset Record by POSTing it to the resource:

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
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "Patched during regular patch window",
        "arc_firmware_version": "3.2.1",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_accepted": "2019-11-27T15:13:21Z",
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "timestamp_committed": "2019-11-27T15:15:02Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
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

.. _firmware_behaviour_UpdateRequired:

Firmware UpdateRequired
...............................................................................

Define the event parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
      "operation": "UpdateRequired",
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "Update to 3.2.1 ASAP",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
      }
    }

.. note::
    attributes.arc_description
        *Required* Details of the Firmware request

    attributes.arc_correlation_value   
        *Optional* Used to link related events together

    timestamp_declared
        *Optional* Client-claimed time at which the maintenance was performed

    principal_declared
        *Optional* Client-claimed identity of person performing the operation

Add the Firmware request to the Asset Record by POSTing it to the resource:

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
      "operation": "UpdateRequired",
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "Update to 3.2.1 ASAP",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_accepted": "2019-11-27T15:13:21Z",
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "timestamp_committed": "2019-11-27T15:15:02Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
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

.. _firmware_behaviour_Vulnerability:

Firmware Vulnerability
...............................................................................

Define the event parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
      "operation": "Vulnerability",
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "All units affected by CVE-2014-0160. Review for risk exposure within reasonable time.",
        "arc_cve_id": "CVE-2014-0160",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
      }
    }

.. note::
    attributes.arc_description
        *Required* Details of the Firmware request

    attributes.cve_id
        *Optional* Track a CVE label against this vulnerability

    attributes.arc_correlation_value   
        *Optional* Used to link related events together

    timestamp_declared
        *Optional* Client-claimed time at which the maintenance was performed

    principal_declared
        *Optional* Client-claimed identity of person performing the operation

Add the Firmware request to the Asset Record by POSTing it to the resource:

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
      "operation": "Vulnerability",
      "behaviour": "Firmware",
      "attributes": {
        "arc_description": "All units affected by CVE-2014-0160. Review for risk exposure within reasonable time."
        "arc_cve_id": "CVE-2014-0160",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_accepted": "2019-11-27T15:13:21Z",
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "timestamp_committed": "2019-11-27T15:15:02Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
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



