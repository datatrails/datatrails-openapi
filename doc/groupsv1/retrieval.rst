
.. _groupsv1_retrieval:

Groups Retrieval (v1)
---------------------

.. include:: ../auth_url.rst

Group membership in Jitsuin Archivist are available via this interface.
The groups are available from the ``groups`` endpoint using the user principal name
as a parameter:

::

    groups/joe.bloggs@acme.com


Fetch Groups for a user principal name
======================================

To fetch all groups for a user  GET the ``groups`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/groups/joe.bloggs@acme.com

This call returns a list of groups for that user:

.. code-block:: JSON

    {
        "groups": [
            {
              "name": "https://sts.windows.net/e6cd7cbd-4331-4942-b28d-xxxxxxxxxxxx/:04a01aa7-9d83-461a-b246-xxxxxxxxxxxx",
              "display_name": "Maintainers"
            },
            {
              "name": "https://sts.windows.net/e6cd7cbd-4331-4942-b28d-xxxxxxxxxxxx/:0d678218-2147-4d3b-a2df-zzzzzzzzzzzz",
              "display_name": "Supervisors"
            },
       ]
    }


.. note::

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1-groups>`_

Fetch All Groups
================

To fetch all groups GET the ``groups`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/groups

This call returns a list of groups:

.. code-block:: JSON

    {
        "groups": [
            {
              "name": "https://sts.windows.net/e6cd7cbd-4331-4942-b28d-xxxxxxxxxxxx/:04a01aa7-9d83-461a-b246-xxxxxxxxxxxx",
              "display_name": "Maintainers"
            },
            {
              "name": "https://sts.windows.net/e6cd7cbd-4331-4942-b28d-xxxxxxxxxxxx/:0bd8e5f1-4788-4b6e-b505-yyyyyyyyyyyy",
              "display_name": "Gurus"
            },
            {
              "name": "https://sts.windows.net/e6cd7cbd-4331-4942-b28d-xxxxxxxxxxxx/:0d678218-2147-4d3b-a2df-zzzzzzzzzzzz",
              "display_name": "Supervisors"
            },
        ]
    }


.. note::

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1-groups>`_
