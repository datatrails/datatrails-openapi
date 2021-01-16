
.. _attachmentsv2_retrieval:

Retrieve Attachment
-------------------

.. note::
   Attachments in the Jitsuin Archivist system are not first-order
   objects in their own right: they are properties of other objects
   such as Asset Records or events. Due to this, Attachments MUST
   be retrieved by providing asset or event identity and unique attachment 
   identity. They cannot be listed, filtered, or searched.

.. include:: ../auth_url.rst

Retrieve a specific Attachment found on an asset assets/c04d5ecf-02e0-4be2-a014-ffbbf0e8ddeb

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/attachments/assets/c04d5ecf-02e0-4be2-a014-ffbbf0e8ddeb/08838336-c357-460d-902a-3aba9528dd22

To retrieve a specific Attachment found on an event assets/c04d5ecf-02e0-4be2-a014-ffbbf0e8ddeb/events/de834094-f6c3-4e38-9b37-8c61dea312c9
issue following curl command

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/attachments/assets/c04d5ecf-02e0-4be2-a014-ffbbf0e8ddeb/events/de834094-f6c3-4e38-9b37-8c61dea312c9/08838336-c357-460d-902a-3aba9528dd22

The response will be a download of the specified attachment

It's also possible to retrieve information about specific attachment using this API.
To do that simply issue request as above with a suffix /info

.. code-block:: shell

    $ curl -v \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/attachments/assets/c04d5ecf-02e0-4be2-a014-ffbbf0e8ddeb/08838336-c357-460d-902a-3aba9528dd22/info

The response will include basic information about the attachment

.. code-block:: JSON

    {
        "identity": "attachments/08838336-c357-460d-902a-3aba9528dd22",
        "hash": {
            "alg": "SHA256",
            "value": "xxxxxxxxxxxxxxxxxxxxxxx"
        },
        "mime_type": "image/jpeg",
        "timestamp_accepted": "2019-11-07T15:31:49Z",
        "size": 31424
    }



