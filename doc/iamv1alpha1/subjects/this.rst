
.. _iamv1alpha1subjects_self:

IAM Subjects Self Entry (v1alpha1)
----------------------------------

There is an immutable entry in the subjects API called "Self" that contains
the keys for the hosting organisation of the Jitsuin Archivist Node.

This entry cannot be deleted or updated.

This special identity is:

::

    subjects/00000000-0000-0000-0000-000000000000


Fetch self IAM Subject by identity (v1alpha1)
=============================================

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/subjects/00000000-0000-0000-0000-000000000000


Response

.. code-block:: JSON

    [
        {
            "identity": "subjects/00000000-0000-0000-0000-000000000000",
            "display_name": "Some description",
            "wallet_pub_key": ["key1"],
            "wallet_address": ["address1"],
            "tessera_pub_key": ["key3"]
        }
    ]

.. note::

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1alpha1-iam-subjects>`_
