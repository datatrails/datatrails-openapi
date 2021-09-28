
.. _tlscacertificatesv1_deletion:

TLS CA Certificate Deletion (v1)
--------------------------------

.. include:: ../auth_url.rst

To delete a TLS CA Certificate, issue following request:

.. code-block:: shell

    $ curl -v -X DELETE \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/v1/tlscacertificates/47b58286-ff0f-11e9-8f0b-362b9e155667

The response is:

.. code-block:: JSON

    {}

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#delete--archivist-tlscacertificates>`_
