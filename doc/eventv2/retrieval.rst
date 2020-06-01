
.. _eventv2_retrieval:

Event Record Retrieval
----------------------

.. include:: ../auth_url.rst

Event records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    assets/12345678-90ab-cdef-1234-567890abcdef/events/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000

If you do not know the event's identity you can fetch event records using other
information you do know, such as the event's name in your asset management or
digital twin platform.


Fetch all events
================

To fetch all event records, simply GET the ``events`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/-/events

Fetch events by asset identity
=======================================

If you know the unique identity of the Asset Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/6a951b62-0a26-4c22-a886-1082297b063b/events

Fetch events by behaviour name
==============================

To fetch all events with a specific behaviour, GET the ``events`` resource and filter on ``behaviour``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/-/events?behaviour=firmware


Fetch events by behaviour name and operation
============================================

To fetch all events with a specific behaviour and operation, GET the ``events`` resource and filter on ``firmware``
and ``update``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/-/events?behaviour=firmware&operation=update


Fetch events by filtering on field names
========================================

To fetch all events with a specific characteristics, GET the ``events`` resource and filter on most available
fields. For example:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/-/events?attributes.arc_firmware_version=1.23

Fetch events by filtering on dates
==================================

To fetch all events occurring at different dates, GET the ``events`` resource and filter on timestamps. For example:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets/-/events?timestamp_accepted_before=2019-12-01T00:00:00Z

Other timestamp filters are
 ``timestamp_accepted_since``,
 ``timestamp_committed_before``,
 ``timestamp_committed_since``,
 ``timestamp_declared_before``,
 ``timestamp_declared_since``.


Responses
=========

Each of these calls returns a list of matching event records in the form:

.. code-block:: JSON

    {
      "identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f/events/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
      "asset_identity": "assets/add30235-1424-4fda-840a-d5ef82c4c96f",
      "behaviour": "Firmware",
      "operation": "Update",
      "attributes": {
        "arc_description": "Patched during regular patch window",
        "arc_firmware_version": "3.2.1",
        "arc_correlation_value": "12-345-67"
      },
      "timestamp_accepted": "2019-11-27T15:13:21Z",
      "timestamp_declared": "2019-11-27T14:44:19Z",
      "timestamp_committed": "2019-11-27T15:15:02Z",
      "principal_declared": {
        "issuer": "idp.synsation.io/1234",
        "subject": "phil.b",
        "email": "phil.b@synsation.io"
      },
      "principal_accepted": {
        "issuer": "job.idp.server/1234",
        "subject": "bob@job"
      },
      "confirmation_status": "CONFIRMED",
      "block_number": 12,
      "transaction_index": 5,
      "transaction_id": "0x07569"
    }


.. note::
    See :ref:`intro_behaviours` and :ref:`intro_lifecycle` for details of how to interpret
    the system-reserved ``arc_*`` attributes.

.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v2-assets>`_
