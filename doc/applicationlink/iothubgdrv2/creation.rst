
.. _iothubgdrv2_creation:

=====================
IoTHubGDR V2 Creation
=====================

.. include:: ../../auth_url.rst

The **iothubgdr** endpoint allows to import all devices from selected Azure IoT Hub into the Jitsuin Archivist system.

Define the iothubgdr parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Jitsuin",
        "secret": "Endpoint=sb://iothub-ns-test-org-1-1637462-0dd952fad8.servicebus.windows.net/;SharedAccessKeyName=iothubowner;SharedAccessKey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx;EntityPath=test-org-1",
        "arc_home_location_identity": "locations/47b575c0-ff0f-11e9-8f0b-362b9e155667"
    }


.. note::
    display_name
        **required**: user-supplied identification of the IotHub GDR 

    secret
        **required**: connection string to Azure IoTHub

    arc_home_location_identity
        **optional**: location identity at which to add the imported devices

    The **iothubgdr** service does not persist the secret.


Post to the endpoint:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v2/iothubgdr

.. _iothubgdrv2_creation_resp:

Responses
-----------

.. code-block:: JSON

    {
        "identity": "iothubgdr/08838336-c357-460d-902a-3aba9528dd22",
        "done": false,
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "timestamp_finished": null,
        "result": {
            "display_name": "Jitsuin",
            "number_assets_imported": 0,
            "arc_home_location_identity": "locations/47b575c0-ff0f-11e9-8f0b-362b9e155667",
            "status": "STATUS_PENDING"
        }
    }

Or in case of error

.. code-block:: JSON

    {
        "identity": "iothubgdr/08838336-c357-460d-902a-3aba9528dd22",
        "done": true,
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "timestamp_finished": "2019-11-07T15:31:55Z",
        "error": {
            "display_name": "Jitsuin",
            "number_assets_imported": 0,
            "arc_home_location_identity": "locations/47b575c0-ff0f-11e9-8f0b-362b9e155667",
            "error_message": "invalid secret provided"
        }
    }

.. note::
    identity
        identifies the iothubgdr.
    
    done
        indicates if the import finished
    
    timestamp_accepted
        date and time when the request has been received
    
    timestamp_finished
        date and time when the import finished (only set when done is set to true)

    result
        returned in absence of error

    display_name
        **part of result**: user-supplied identification of the IotHub GDR 

    number_assets_imported
        **part of result**: indicates number of assets imported so far

    arc_home_location_identity
        **part of result**: location identity at which to add the imported devices

    status
        **part of result**: one of STATUS_PENDING, STATUS_INPROGRESS, STATUS_FINISHED, STATUS_CANCELLED
        indicates current status of the import
    
    error
        returned only if the import resulted in error

    display_name
        **part of error**: user-supplied identification of the IotHub GDR 

    number_assets_imported
        **part of error**: indicates number of assets imported so far

    location_identity
        **part of error**: location identity at which to add the imported devices
    
    error_message
        **part of error**: short description of an error

.. note::
    See `Swagger POST API <openapi.html#post --archivist-v2-iothubgdr>`_
