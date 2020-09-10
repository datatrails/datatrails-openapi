
.. _compliance:

Compliance
-----------

.. include:: ../auth_url.rst

The **compliancev1** endpoint reports on the status of compliance with Compliance Policies.

Query the endpoint:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/compliance/assets/6a951b62-0a26-4c22-a886-1082297b063b


The response is:

.. code-block:: JSON

    {
        "compliant": true,
        "compliance": [
            {
                "compliance_policy_identity": "compliance_policies/0000-0000-000000000-00000000",
                "compliant": true
            }
        ]
    }

.. note::
    compliant
        overall compliance status, false if any Compliance Policy "compliant" is false.  True if all Compliance Policy "compliant" are true.

    The response contains a list of Compliance Statements.

    Each member of the list has the following attributes:

    compliance_policy_identity
        The identity of the Compliance Policy this statement refers to.

    compliant
        Compliance status for this Compliance Policy.

    See `Swagger GET API <openapi.html#get --archivist-v1-compliance>`_

