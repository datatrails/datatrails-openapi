
.. _tlscacertificatesv1_retrieval:

TLS CA Certificate Retrieval (v1)
---------------------------------

.. include:: ../auth_url.rst

TLS CA Certificate records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    tlscacertificates/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the certificate's identity you can fetch TLS CA Certificate records using other
information you do know, such as the certificate's name.


Fetch all TLS CA Certificates (v1)
==================================

To fetch all TLS CA certificates records, simply GET the ``tlscacertificates`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/tlscacertificates

Fetch specific TLS CA Certificate by identity (v1)
==================================================

If you know the unique identity of the TLS CA certificate Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/tlscacertificates/6a951b62-0a26-4c22-a886-1082297b063b

Fetch TLS CA Certificates by name (v1)
======================================

To fetch all TLS CA Certificates with a specific name,  GET the ``tlscacertificates`` resource and filter on ``display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/tlscacertificates?display_name=Acme


Each of these calls returns a list of matching TLS CA Certificate records in the form (certificate field shortened for brevity):

.. code-block:: JSON

    {
        "certificates": [
            {
                "identity": "tlscacertificates/6a951b62-0a26-4c22-a886-1082297b063b",
                "display_name": "Some description",
                "certificate": "-----BEGIN CERTIFICATE----- MIIEBDCCAuygAwIBAgIDAjppMA0GCSqGSIb3DQEBBQUAMEIxCzAJBgNVBAYTAlVT -----END CERTIFICATE----- "
            },
            {
                "identity": "tlscacertificates/12345678-0a26-4c22-a886-1082297b063b",
                "display_name": "Some other description",
                "certificate": "-----BEGIN CERTIFICATE----- XYZEBDCCAuygAwIBAgIDAjppMA0GCSqGSIb3DQEBBQUAMEIxCzAJBgNVBAYTAlVT -----END CERTIFICATE----- "
            }
        ]
    }

.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

.. note::

   The total number of certificates that exist is returned in the response header field 'x-total-count' if
   the 'x-request-total-count' header on the request is set to 'true'.
   The curl option '-i' will emit this to stdout.

.. note::

   A full API reference is available in `Swagger GET API <openapi.html#get--archivist-tlscacertificates>`_
