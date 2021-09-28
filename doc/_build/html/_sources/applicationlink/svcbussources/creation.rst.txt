
.. _svcbussources_creation:

SvcBusSources Creation
----------------------

.. include:: ../../auth_url.rst

The **svcbussources** endpoint allows subscribing to an Azure Service Bus Queue and receiving events
when a device changes state. The state changes are recorded in the Jitsuin Archivist system.

The servicebus connection string is obtained from here :ref:`subscription_connection_string`.

.. warning::
    The connection string used is for the **servicebus** and not for the **servicebus queue**.


Define the svcbussource parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Jitsuin",
        "connection_string": "Endpoint=sb://jitsuin-dev.servicebus.windows.net/;SharedAccessKeyName=jitsuin-listener;SharedAccessKey=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "queue_name": "jitsuin-listener"
    }


.. note::
    display_name
        **required**: user-supplied identification of the IotHub subscription 

    connection_string
        **required**: connection string to Azure Service bus. This will be
        stored in a secure keyvault.

    queue_name
        **required**: user-configured Azure service bus queue name

    The **svcbussources** service is capacity limited to 2 subscriptions. Attempting to
    create a third subscription will return a 429 code (ResourceExhausted)

	No error will be returned if the subscription fails to connect to the endpoint.

Post to the endpoint:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/svcbussources


The response is:

.. code-block:: JSON

    {
        "identity": "svcbussources/08838336-c357-460d-902a-3aba9528dd22",
        "display_name": "Jitsuin",
        "queue_name": "jitsuin-listener"
    }

.. note::
    identity
        identifies the svcbussource subscription.

    display_name
       	user-supplied identification of the IotHub subscription 

    queue_name
       	user-configured Azure service bus queue 

.. note::
    See `Swagger POST API <openapi.html#post --archivist-v1-svcbussources>`_
