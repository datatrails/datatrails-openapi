
.. _tlscacertificatesv1_upload:

TLS CA Certificates Upload (v1)
--------------------------------

.. include:: ../auth_url.rst

Define the TLS CA certificate parameters and store in /path/to/jsonfile (certificate field shortened for brevity):

.. code-block:: JSON

    {
        "display_name": "Some description",
        "certificate": "-----BEGIN CERTIFICATE-----\nMIIFxDCCA6ygAwIBAgIBAjANBgkqhkiG9w0BAQsFADCBsDELMAkGA1UEBhMCVVMx\nETAPBgNV....1NF/BjDZ4wdexw==\n-----END CERTIFICATE-----\n"
    }

To include the PEM file content in a JSON string it must be flattened to a
single line. To create a single line representation of a PEM file for the
archivist api, you must replace new lines with the literal string "\n". The
following unix command could be used:

.. code-block:: shell

    $ awk 'NF {sub(/\r/, ""); printf "%s\\n",$0;}' cert-name.pem

.. note::
    display_name
        **required** Friendly name for the location. Displayed in the Archivist GUI.

    certificate
        **required** Single line "flattened" PEM containing a CERTIFICATE.

Create the CA Certificate:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/tlscacertificates


The response is (certificate field shortened for brevity):

.. code-block:: JSON

    {
        "identity": "tlscacertificates/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
        "certificate": "-----BEGIN CERTIFICATE----- MIIEBDCCAuygAwIBAgIDAjppMA0GCSqGSIb3DQEBBQUAMEIxCzAJBgNVBAYTAlVT -----END CERTIFICATE-----"
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-tlscacertificates>`_
