
.. _assetv2_creation:

Asset Record Creation
---------------------

.. include:: ../auth_url.rst

Define the asset parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "behaviours": ["Firmware", "Maintenance", "RecordEvidence", "LocationUpdate", "Attachments"],
        "attributes": {
            "arc_firmware_version": "1.0",
            "arc_serial_number": "vtl-x4-07",
            "arc_display_name": "tcl.ppj.003",
            "arc_description": "Traffic flow control light at A603 North East",
            "arc_home_location_identity": "locations/115340cf-f39e-4d43-a2ee-8017d672c6c6",
            "arc_display_type": "Traffic light with violation camera",
            "arc_primary_image": "attachments/87b1a84c-1c6f-442b-923e-a97516f4d275",
            "some_custom_attribute": "value"
        }
    }

.. note::
    behaviours
        list of behaviours to enable for this asset

    attributes
        properties of asset

    See :ref:`intro_behaviours` for details of behaviours and the system-
    reserved ``arc_*`` attributes.

    See :ref:`attachments_upload`, :ref:`locations_creation`, and
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
            "Firmware",
            "Maintenance",
            "RecordEvidence",
            "LocationUpdate",
            "Attachments"
        ],
        "attributes": {
            "arc_serial_number": "vtl-x4-07",
            "arc_display_name": "tcl.ppj.003",
            "arc_description": "Traffic flow control light at A603 North East",
            "arc_home_location_identity": "locations/115340cf-f39e-4d43-a2ee-8017d672c6c6",
            "arc_display_type": "Traffic light with violation camera",
            "arc_firmware_version": "1.0",
            "arc_primary_image": "attachments/87b1a84c-1c6f-442b-923e-a97516f4d275",
            "some_custom_attribute": "value"
        },
        "confirmation_status": "PENDING",
        "tracked": "TRACKED"
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v2-assets>`_

