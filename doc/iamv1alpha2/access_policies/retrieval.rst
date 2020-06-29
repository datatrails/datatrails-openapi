
.. _iamv1alpha2access_policies_retrieval:

IAM Access Policies Retrieval (v1alpha2)
----------------------------------------

.. include:: ../../auth_url.rst

IAM access policy records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    access_policies/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the access_policy's identity you can fetch IAM access policy records using other
information you do know, such as the access_policy's name.


Fetch all IAM access_policies (v1alpha2)
========================================

To fetch all IAM access_policies records, simply GET the ``iam/access_policies`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha2/iam/access_policies

Fetch specific IAM access Policy by identity (v1alpha2)
=======================================================

If you know the unique identity of the IAM access policy Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha2/iam/access_policies/6a951b62-0a26-4c22-a886-1082297b063b

Fetch IAM Access Policies by name (v1alpha2)
============================================

To fetch all IAM access_policies with a specific name,  GET the ``iam/access_policies`` resource and filter on ``display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha2/iam/access_policies?display_name=Some%20description


Each of these calls returns a list of matching IAM access_policies records in the form:

.. code-block:: JSON

    {
        "access_policies": [
            {
                "identity": "access_policies/6a951b62-0a26-4c22-a886-1082297b063b",
                "display_name": "Some description",
                "filters":"[
                    [
                        \"attributes.arc_home_location_identity=locations/5ea815f0-4de1-4a84-9377-701e880fe8ae\",
                        \"attributes.arc_home_location_identity=locations/27eed70b-9e2b-4db1-b8c4-e36505350dcc\",
                    ],
                    [
                        \"attributes.arc_display_type=Valve\",
                        \"attributes.arc_display_type=Pump\"
                    ],
                    [
                        \"attributes.ext_vendor_name=SynsationIndustries\"
                    ]
                ]",
                "access_permissions": [
                    {
                        "subjects": [
                            "subjects/6a951b62-0a26-4c22-a886-1082297b063b",
                            "subjects/a24306e5-dc06-41ba-a7d6-2b6b3e1df48d"
                        ],
                        "behaviours": [  "Attachments", "Firmware", "Maintenance", "RecordEvidence"  ],
                        "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ]
                    }
                ]
            },
            {
                "identity": "access_policies/12345678-0a26-4c22-a886-1082297b063b",
                "display_name": "Some other description",
                "filters": "[
                    [\"attributes.arc_display_type=door_access_reader\"]
                ]",
                "access_permissions": [
                    {
                        "subjects": [
                            "subjects/6a951b62-0a26-4c22-a886-1082297b063b",
                            "subjects/a24306e5-dc06-41ba-a7d6-2b6b3e1df48d"
                        ],
                        "behaviours": [ "Attachments", "Maintenance", "RecordEvidence" ],
                        "include_attributes": [ "arc_display_name", "arc_display_type" ]
                    }
                ]
            }
        ]
    }


.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1alpha2-iam-access_policies>`_
