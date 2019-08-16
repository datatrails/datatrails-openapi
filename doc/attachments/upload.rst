
.. _attachments_upload:

Upload Attachment
-----------------

.. include:: ../auth_url.rst


Upload the attachment stored at /path/to/file:

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        -F "file=@/path/to/file" \
        $URL/archivist/v1/attachments

.. note::

  See `Swagger POST API <openapi.html#post--archivist-v1-attachments>`_


The response is:

.. code-block:: JSON

    {
        "identity": "attachments/08838336-c357-460d-902a-3aba9528dd22",
        "timestamp_accepted": "Macclesfield, Cheshire",
        "hash": {
            "algorithm": "SHA256",
            "value": "xxxxxxxxxxxxxxxxxxxxxxx",
        },
        "size": 1234567,
        "mime_type": "application/jpeg"
    }


.. note::
   The **"identity"** field is used to reference the attachment to an asset during asset
   creation or asset event. (usually a maintenance event).

