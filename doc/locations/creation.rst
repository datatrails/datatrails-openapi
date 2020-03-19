
.. _locations_creation:

Location Creation
-----------------

.. include:: ../auth_url.rst

Define the location parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
       "display_name": "Macclesfield, Cheshire",
       "description": "Manufacturing site, North West England, Macclesfield, Cheshire",
       "latitude": 53.2546799,
       "longitude": -2.1213956,
       "attributes": {
           "director": "John Smith",
           "address": "Unit 6A, Synsation Park, Maccelsfield",
           "Facility Type": "Manufacture",
           "support_email": "support@macclesfield.com",
           "support_phone": "123 456 789"
        }
    }

.. note::
    display_name
        **required** Friendly name for the location. Displayed in the Archivist GUI.

    description
        **required** Extended information about the location.

    extended_attributes
        freeform and can contain any fields.

    See `Swagger POST API <openapi.html#post--archivist-v1-locations>`_

Create the location to POSTing to the ``locations`` resource:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v2/locations


The response is:

.. code-block:: JSON

    {
        "identity": "locations/08838336-c357-460d-902a-3aba9528dd22",
        "display_name": "Macclesfield, Cheshire",
        "description": "Manufacturing site, North West England, Macclesfield, Cheshire",
        "latitude": 53.2546799,
        "longitude": -2.1213956,
        "attributes": {
            "director": "John Smith",
            "address": "Bridgewater, Somerset",
            "Facility Type": "Manufacture",
            "support_email": "support@macclesfield.com",
            "support_phone": "123 456 789"
        }
    }

.. note::
    identity
        used to attach the location to an asset during asset
        creation or asset event. (usually a maintenance event).

