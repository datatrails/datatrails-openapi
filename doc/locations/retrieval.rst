
.. _locations_retrieval:

Location Retrieval
------------------

.. include:: ../auth_url.rst

Fetch all locations
===================

To fetch all locations, simply GET the ``locations`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/locations

Fetch specific location by identity
===================================

If you know the unique identity of the location record, simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/locations/08838336-c357-460d-902a-3aba9528dd22


Fetch location by name
======================

To fetch all locations with a specific name,  GET the ``assets`` resource and
filter on ``display_name``:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/locations?display_name=Macclesfield%2C%20Cheshire

.. note::
   It is advisable to implement a unique naming scheme for location names,
   but this is not enforced by the system. If multiple locations exist with
   the same name they will all be returned, and the client will need to
   differentiate based on other attributes.


Each of these calls returns a list of matching asset records in the form:

.. code-block:: JSON

    {
        "locations": [
            {
                "identity": "locations/08838336-c357-460d-902a-3aba9528dd22",
                "display_name": "Macclesfield, Cheshire",
                "description": "Manufacturing site, North West England, Macclesfield, Cheshire",
                "latitude": "53.2546799",
                "longitude": "-2.1213956,14.54",
                "attributes": {
                    "director": "John Smith",
                    "address": "Bridgewater, Somerset",
                    "Facility Type": "Manufacture",
                    "support_email": "support@macclesfield.com",
                    "support_phone": "123 456 789"
                }
            }
        ]
    }

