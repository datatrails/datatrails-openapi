
.. _blobsV1_upload:

Upload Blob
-----------

.. include:: ../auth_url.rst


Upload the blob stored at /path/to/file:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "content_type=image/jpg" \
        -F "file=@/path/to/file" \
        $URL/archivist/v1/blobs


The response is:

.. code-block:: JSON

    {
        "identity": "blobs/08838336-c357-460d-902a-3aba9528dd22",
        "hash": {
            "alg": "SHA256",
            "value": "xxxxxxxxxxxxxxxxxxxxxxx"
        },
        "mime_type": "image/jpeg",
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "size": 31424
    }


.. note::
   identity
       The unique identity of the asset in the Jitsuin Archivist system,
       used to reference the blob in an Asset Record or asset event
       (usually a Maintenance event).

.. warning::
       Blobs in the Jitsuin Archivist system are not first-order
       objects in their own right: they are properties of other objects
       such as Asset Records or events.

