
.. _locations_creation:

Location Creation
-----------------

.. include:: ../auth_url.rst

Define the location parameters and store in /path/to/jsonfile:

.. code-block:: JSON

    {
       "display_name": "Macclesfield, Cheshire",
       "description": "Manufacturing site, North West England, Macclesfield, Cheshire",
       "latitude": "53.2546799",
       "longitude": "-2.1213956,14.54",
       "extended_attributes": {
       "director": "John Smith",
       "address": "Bridgewater, Somerset",
       "Facility Type": "Manufacture",
           "support_email": "support@macclesfield.com",
           "support_phone": "123 456 789"
        }
    }

.. note::
    The **"display_name"** field is **required**.

    The **"description"** field is **required**.

    The **"extended_attributes"** fields are freeform and can contain any fields.

   See `Swagger POST API <openapi.html#post--archivist-v1-locations>`_

Create the location:

.. code-block:: shell

    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/locations


The response is:

.. code-block:: JSON

    {
        "identity": "locations/08838336-c357-460d-902a-3aba9528dd22",
        "display_name": "Macclesfield, Cheshire",
        "description": "Manufacturing site, North West England, Macclesfield, Cheshire",
        "latitude": "53.2546799",
        "longitude": "-2.1213956,14.54",
        "extended_attributes": {
            "director": "John Smith",
            "address": "Bridgewater, Somerset",
            "Facility Type": "Manufacture",
            "support_email": "support@macclesfield.com",
            "support_phone": "123 456 789"
        }
    }

.. note::
   The **"identity"** field is used to attach the location to an asset during asset
   creation or asset event. (usually a maintenance event).

