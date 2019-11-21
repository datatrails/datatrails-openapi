
.. _svcbussources_delete:

SvcBusSources Deletion
----------------------

.. include:: ../../auth_url.rst

The **svcbussources** endpoint allows subscribing to the Azure Service Bus Queue and receiving events
when a device changes state. The state changes are recorded in the Jitsuin Archivist system.

Delete the endpoint:

.. code-block:: shell

    $ curl -v -X DELETE \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/svcbussources/08838336-c357-460d-902a-3aba9528dd22


The response is:

.. code-block:: JSON

    {
        "identity": "svcbussources/08838336-c357-460d-902a-3aba9528dd22",
        "display_name": "Jitsuin",

    }

.. note::
    identity
        identifies the iothubsubscriber subscription.

    display_name
		user supplied identification of the IotHub subscription

    queue_name
        user-configured Azure service bus queue

    See `Swagger DELETE API <openapi.html#delete --archivist-v1-svcbussources>`_

