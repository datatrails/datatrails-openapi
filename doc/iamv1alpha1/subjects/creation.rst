
.. _iamv1alpha1subjects_creation:

IAM Subjects Creation (v1alpha1)
--------------------------------

.. include:: ../../auth_url.rst

Define the subjects parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Some description",
        "wallet_pub_key": ["key1"],
        "tessera_pub_key": ["key2"]
    }

.. note::
    display_name
        **required** Friendly name for the location. Displayed in the Archivist GUI.

    wallet_pub_key
        **required** a list containing a single organisation wallet key.

    tessera_pub_key
        **required** a list containing the single tessera key for the archivist node the subject has residency on

Create the IAM subject:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1alpha1/iam/subjects


The response is:

.. code-block:: JSON

    {
        "identity": "subjects/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
        "wallet_pub_key": ["key1"],
        "wallet_address": ["address"],
        "tessera_pub_key": ["key2"]
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v1alpha1-iam-subjects>`_
