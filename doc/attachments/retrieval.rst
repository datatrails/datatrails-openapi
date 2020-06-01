
.. _attachments_retrieval:

Retrieve Attachment
-------------------

.. note::
   Attachments in the Jitsuin Archivist system are not first-order
   objects in their own right: they are properties of other objects
   such as Asset Records or events. Due to this, Attachments MUST
   be retrieved by full unique resource identity as stored in an
   asset Record or Event property. They cannot be listed, filtered,
   or searched.

.. include:: ../auth_url.rst

Retrieve a specific Attachment

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        -H "content_type=image/jpg" \
        -F "file=@/path/to/file" \
        $URL/archivist/v1/attachments/08838336-c357-460d-902a-3aba9528dd22


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

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v2-attachments>`_


