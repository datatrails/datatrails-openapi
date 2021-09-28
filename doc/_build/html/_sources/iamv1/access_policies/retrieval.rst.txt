
.. _iamv1access_policies_retrieval:

IAM Access Policies Retrieval (v1)
----------------------------------------

.. include:: ../../auth_url.rst

IAM access policy records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    access_policies/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the access_policy's identity you can fetch IAM access policy records using other
information you do know, such as the access_policy's name.


Fetch all IAM access_policies (v1)
========================================

To fetch all IAM access_policies records, simply GET the ``iam/access_policies`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/iam/v1/access_policies

Fetch specific IAM access Policy by identity (v1)
=======================================================

If you know the unique identity of the IAM access policy Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/iam/v1/access_policies/6a951b62-0a26-4c22-a886-1082297b063b

Fetch IAM Access Policies by name (v1)
============================================

To fetch all IAM access_policies with a specific name,  GET the ``iam/access_policies`` resource and filter on ``display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/iam/v1/access_policies?display_name=Some%20description


Each of these calls returns a list of matching IAM access_policies records in the form:

.. code-block:: JSON

    {
        "access_policies": [
            {
                "identity": "access_policies/6a951b62-0a26-4c22-a886-1082297b063b",
                "display_name": "Name to display",
                "description": "Description of the policy",
                "filters": [
                    {"or": [
                        "attributes.arc_home_location_identity=locations/5ea815f0-4de1-4a84-9377-701e880fe8ae",
                        "attributes.arc_home_location_identity=locations/27eed70b-9e2b-4db1-b8c4-e36505350dcc"
                    ]},
                    {"or": [
                        "attributes.arc_display_type=Valve",
                        "attributes.arc_display_type=Pump"
                    ]},
                    {"or": [
                        "attributes.ext_vendor_name=SynsationIndustries"
                    ]}
                ],
                "access_permissions": [
                    {
                        "asset_attributes_read": [ "toner_colour", "toner_type" ],
                        "asset_attributes_write":["toner_colour"],
                        "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                        "event_arc_display_type_read": ["toner_type", "toner_colour"],
                        "event_arc_display_type_write": ["toner_replacement"],
                        "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ],
                        "subjects": [
                            "subjects/6a951b62-0a26-4c22-a886-1082297b063b",
                            "subjects/a24306e5-dc06-41ba-a7d6-2b6b3e1df48d"
                        ],
                        "user_attributes": [
                            {"or": ["group:maintainers", "group:supervisors"]}
                        ]
                    }
                ]
            },
            {
                "identity": "access_policies/12345678-0a26-4c22-a886-1082297b063b",
                "display_name": "Some other description",
                "filters": [
                    {"or": ["attributes.arc_display_type=door_access_reader"]}
                ],
                "access_permissions": [
                    {
                        "asset_attributes_read": [ "toner_colour", "toner_type" ],
                        "asset_attributes_write":["toner_colour"],
                        "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                        "event_arc_display_type_read": ["toner_type", "toner_colour"],
                        "event_arc_display_type_write": ["toner_replacement"],
                        "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ],
                        "subjects": [
                            "subjects/6a951b62-0a26-4c22-a886-1082297b063b",
                            "subjects/a24306e5-dc06-41ba-a7d6-2b6b3e1df48d"
                        ],
                        "user_attributes": [
                            {"or": ["group:maintainers", "group:supervisors"]}
                        ]
                    }
                ]
            }
        ]
    }


.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

.. note::

   The total number of assets that exist is returned in the response header field 'x-total-count' if
   the 'x-request-total-count' header on the request is set to 'true'.
   The curl option '-i' will emit this to stdout.

.. note::

   A full API reference is available in `Swagger GET API <openapi.html#get--archivist-iam-v1-access_policies>`_
