
.. _iamv1alpha1access_policies_creation:

IAM Access Policies Creation (v1alpha1)
---------------------------------------

.. include:: ../../auth_url.rst

Define the access_policies parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
        "display_name": "Some description",
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
                "access_keys": [
                    {
                        "tessera": [ "key1", "key2" ],
                        "wallet": [ "key3", "key4" ]
                    },
                    {
                        "tessera": [ "key5", "key6" ],
                        "wallet": [ "key7", "key8" ]
                    }
                ],
                "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ]
            }
        ]
    }

.. note::
    display_name
        **required** Friendly name for the location. Displayed in the Archivist GUI.

    filters
        String containing JSON of a list of lists of asset attributes to match.
        Note the need to escape strings in this field ONLY.

    access_permissions
        A list specifying which rights apply to which subjects for the matching
        assets.

        access_keys
            list of maps of wallet and tessera keys for the subjects to be granted
            these rights 

        behaviours
            list of behaviours to allow for those subjects

        include_attributes
            list of attributes to share with those subjects

Create the access policy:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1alpha1/iam/access_policies


The response is:

.. code-block:: JSON

    {
        "identity": "access_policies/3f5be24f-fd1b-40e2-af35-ec7c14c74d53",
        "display_name": "Some description",
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
                "access_keys": [
                    {
                        "tessera": [ "key1", "key2" ],
                        "wallet": [ "key3", "key4" ]
                    },
                    {
                        "tessera": [ "key5", "key6" ],
                        "wallet": [ "key7", "key8" ]
                    }
                ],
                "behaviours": [ "Attachments", "Firmware", "Maintenance", "RecordEvidence" ],
                "include_attributes": [ "arc_display_name", "arc_display_type", "arc_firmware_version" ]
            }
        ]
    }

.. note::

    A full API reference is available in `Swagger POST API <openapi.html#post--archivist-v1alpha1-iam-access_policies>`_
