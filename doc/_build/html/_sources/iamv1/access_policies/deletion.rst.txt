
.. _iamv1access_policies_deletion:

IAM Access Policy Deletion (v1)
-------------------------------------

.. include:: ../../auth_url.rst

To delete an IAM access policy, issue following request:

.. code-block:: shell

    $ curl -v -X DELETE \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        $URL/archivist/iam/v1/access_policies/47b58286-ff0f-11e9-8f0b-362b9e155667

The response is:

.. code-block:: JSON

    {}

.. note::

    A full API reference is available in `Swagger DELETE API <openapi.html#delete--archivist-iam-v1-identity>`_
