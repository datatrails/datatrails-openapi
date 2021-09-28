
.. _blobsV1_retrieval:

Retrieve Blob
-------------

.. note::
   Blobs in the Jitsuin Archivist system are not first-order
   objects in their own right: they are properties of other objects
   such as Asset Records or events.

.. include:: ../auth_url.rst

Retrieve a specific Attachment

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        -H "content_type=image/jpg" \
        -F "file=@/path/to/file" \
        $URL/archivist/v1/blobs/08838336-c357-460d-902a-3aba9528dd22


The response is:

.. code-block:: JSON

    {
        "identity": "blobsV1/08838336-c357-460d-902a-3aba9528dd22",
        "hash": {
            "alg": "SHA256",
            "value": "xxxxxxxxxxxxxxxxxxxxxxx"
        },
        "mime_type": "image/jpeg",
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "size": 31424
    }

