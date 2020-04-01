
.. _iothubgdrv2_management:

IoTHubGDR V2 Management
-----------------------

.. include:: ../../auth_url.rst

The **iothubgdr** endpoint allows to query and manage recent imports.

To list all imports issue following GET request:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/v2/iothubgdr

This call will respond with a list containing all known imports.
Individual items in list are identical to create :ref:`iothubgdrv2_creation_resp`

To get specific import details (identity of the import has to be known in order to issue that request - for this example assume `47b58286-ff0f-11e9-8f0b-362b9e155667`) issue following request:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/v2/iothubgdr/47b58286-ff0f-11e9-8f0b-362b9e155667

Response has the same format as create :ref:`iothubgdrv2_creation_resp`

To cancel running import issue following request:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/v2/iothubgdr/47b58286-ff0f-11e9-8f0b-362b9e155667:cancel

Response has the same format as create response but the status is set to `STATUS_CANCELLED`

To delete an import issue following request:

.. code-block:: shell

    $ curl -v -X DELETE \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/v2/iothubgdr/47b58286-ff0f-11e9-8f0b-362b9e155667

Import will be deleted from tracked imports but the underlying job will not stop. To stop the job
cancel it before deleting.

Response to successful deletion is empty `{}`.

.. note::
    See `Swagger POST API <openapi.html#post --archivist-v2-iothubgdr>`_
