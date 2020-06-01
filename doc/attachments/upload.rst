
.. _attachments_upload:

Upload Attachment
-----------------

.. include:: ../auth_url.rst


Upload the attachment stored at /path/to/file:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "content_type=image/jpg" \
        -F "file=@/path/to/file" \
        $URL/archivist/v1/attachments


The response is:

.. code-block:: JSON

    {
        "identity": "attachments/08838336-c357-460d-902a-3aba9528dd22",
        "hash": {
            "algorithm": "SHA256",
            "value": "xxxxxxxxxxxxxxxxxxxxxxx"
        },
        "mime_type": "image/jpeg",
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "size": 31424
    }


.. note::
   identity
       The unique identity of the asset in the Jitsuin Archivist system,
       used to reference the attachment in an Asset Record or asset event
       (usually a Maintenance event).

.. warning::
       Attachments in the Jitsuin Archivist system are not first-order
       objects in their own right: they are properties of other objects
       such as Asset Records or events. Due to this, Attachments
       cannot be listed, filtered or searched, so it is important that
       you remember the attachment identity returned until you connect
       it to a suitable Asset Record or Event.


.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v2-attachments>`_

~                                                                                                                                      
