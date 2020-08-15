
.. _iamv1alpha2access_policies_creation:

IAM Access Policies Creation (v1alpha2)
---------------------------------------

.. include:: ../../auth_url.rst

Define the access_policies parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Name to display",
        "description": "Description of the policy",
        "filters": "[
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
                "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ],
                "user_attributes": [
                    {"or": ["group:maintainers", "group:supervisors"]}
                ]
            }
        ]
    }

.. note::
    display_name
        **required** Friendly name for the policy. Displayed in the Archivist GUI.

    description
        Description of the policy.


    filters
        String containing JSON of a list of lists of asset attributes to match.
        Note the need to escape strings in this field ONLY.

    access_permissions
        A list specifying which rights apply to which subjects for the matching
        assets.

        subjects
            list of subject identities of subjects to be granted
            these rights 

        behaviours
            list of behaviours to allow for those subjects

        include_attributes
            list of attributes to share with those subjects

        user_attributes
            list of user attribute filters that specifies who is allowed to see this asset

Create the access policy:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1alpha2/iam/access_policies


The response is:

.. code-block:: JSON

    {
        "identity": "access_policies/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Friendly name of the policy",
        "description": "Description of the policy",
        "filters": "[
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
                "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ],
                "user_attributes": [
                    {"or": ["group:maintainers", "group:supervisors"]}
                ]
            }
        ]
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v1alpha2-iam-access_policies>`_
