
.. _assetv2_retrieval:

Asset Record Retrieval
----------------------

.. include:: ../auth_url.rst

Asset records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    assets/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the asset's identity you can fetch asset records using other
information you do know, such as the asset's name in your asset management or
digital twin platform.


Fetch all assets
================

To fetch all asset records, simply GET the ``assets`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets

Fetch specific asset by identity
================================

If you know the unique identity of the Asset Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/6a951b62-0a26-4c22-a886-1082297b063b

Fetch assets by name
====================

To fetch all assets with a specific name,  GET the ``assets`` resource and filter on ``arc_display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets?attributes.arc_display_name=tcl.ccj.003

Fetch assets by type
====================

To fetch all assets of a specific type,  GET the ``assets`` resource and filter on ``arc_display_type``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets?attributes.arc_display_type=Traffic%20light

Each of these calls returns a list of matching asset records in the form:

.. code-block:: JSON

    {
        "assets": [
            {
            "identity": "assets/6a951b62-0a26-4c22-a886-1082297b063b",
            "behaviours": [
                "Firmware",
                "Maintenance",
                "RecordEvidence",
                "LocationUpdate",
                "Attachments"
            ],
            "attributes": {
                "arc_display_type": "Traffic light",
                "arc_firmware_version": "1.0",
                "arc_home_location_identity": "locations/866790d8-4ed6-4cc9-8f60-07672609b331",
                "arc_serial_number": "vtl-x4-07",
                "arc_description": "Traffic flow control light at A603 North East",
                "arc_display_name": "tcl.ccj.003",
                "arc_primary_image_identity": "attachments/87b1a84c-1c6f-442b-923e-a97516f4d275",
                "some_custom_attribute": "value"
            },
            "confirmation_status": "CONFIRMED",
            "tracked": "TRACKED"
            }
        ]
    }

Fetch assets by filtering for presence of a field
=================================================

To fetch all assets with a field set to any value,  GET the ``assets`` resource
and filter on most available fields. For example:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets?attributes.arc_display_name=*

Returns all assets which have arc_display_name that is not empty.

Fetch assets which are missing a field
======================================

To fetch all assets with a field which is not set to any value,  GET the
``assets`` resource and filter on most available fields. For example:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets?attributes.arc_display_name!=*

Returns all assets which do not have arc_display_name or in which
arc_display_name is empty.

.. note::
    See :ref:`intro_behaviours` and :ref:`intro_lifecycle` for details of how to interpret
    the system-reserved ``arc_*`` attributes.

    See :ref:`attachments_upload` and/or :ref:`locations_creation` for details
    of how to handle the ``arc_home_location_identity`` and ``arc_primary_image_identity``
    attributes.

.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v2-assets>`_
