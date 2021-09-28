
.. _tlscacertificatesv1_update:

TLS CA Certificates Update (v1)
-------------------------------

.. include:: ../auth_url.rst

Define the TLS CA certificates parameters to be changed and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "new description"
    }

.. note::

    display_name
        descriptive name of TLS CA certificate

Update the TLS CA Certificate:

.. code-block:: shell

    $ curl -v -X PATCH \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/tlscacertificates/47b58286-ff0f-11e9-8f0b-362b9e155667


The response is (certificate field shortened for brevity):

.. code-block:: JSON

    {
        "identity": "tlscacertificates/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
        "certificate": "-----BEGIN CERTIFICATE----- MIIEBDCCAuygAwIBAgIDAjppMA0GCSqGSIb3DQEBBQUAMEIxCzAJBgNVBAYTAlVT -----END CERTIFICATE-----"
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#patch--archivist-tlscacertificates>`_
