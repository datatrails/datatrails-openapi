
.. _assetv2_creation:

Asset Record Creation
---------------------

.. include:: ../auth_url.rst

Define the asset parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "behaviours": ["RecordEvidence"],
        "attributes": {
            "arc_firmware_version": "1.0",
            "arc_serial_number": "vtl-x4-07",
            "arc_display_name": "tcl.ppj.003",
            "arc_description": "Traffic flow control light at A603 North East",
            "arc_home_location_identity": "locations/115340cf-f39e-4d43-a2ee-8017d672c6c6",
            "arc_display_type": "Traffic light with violation camera",
            "some_custom_attribute": "value",
            "arc_attachments": [
                {
                    "arc_display_name": "arc_primary_image",
                    "arc_attachment_identity": "blobs/87b1a84c-1c6f-442b-923e-a97516f4d275",
                    "arc_hash_alg": "SHA256",
                    "arc_hash_value": "246c316e2cd6971ce5c83a3e61f9880fa6e2f14ae2976ee03500eb282fd03a60"
                }
            ]
        }
    }

.. note::
    behaviours
        list of behaviours to enable for this asset

    attributes
        properties of asset

    See :ref:`intro_behaviours` for details of behaviours and the system-
    reserved ``arc_*`` attributes.

    See :ref:`blobsv1_upload`, :ref:`locations_creation`, and
    :ref:`locations_retrieval` for details of how to get the correct values
    for  ``arc_home_location_identity`` and ``arc_primary_image``.

Create the asset:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v2/assets


The response is:

.. code-block:: JSON

    {
        "identity": "assets/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "behaviours": [
            "RecordEvidence"
        ],
        "attributes": {
            "arc_serial_number": "vtl-x4-07",
            "arc_display_name": "tcl.ppj.003",
            "arc_description": "Traffic flow control light at A603 North East",
            "arc_home_location_identity": "locations/115340cf-f39e-4d43-a2ee-8017d672c6c6",
            "arc_display_type": "Traffic light with violation camera",
            "arc_firmware_version": "1.0",
            "some_custom_attribute": "value",
            "arc_attachments": [
                {
                    "arc_display_name": "arc_primary_image",
                    "arc_attachment_identity": "blobs/87b1a84c-1c6f-442b-923e-a97516f4d275",
                    "arc_hash_alg": "SHA256",
                    "arc_hash_value": "246c316e2cd6971ce5c83a3e61f9880fa6e2f14ae2976ee03500eb282fd03a60"
                }
            ]
        },
        "confirmation_status": "PENDING",
        "tracked": "TRACKED"
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v2-assets>`_
