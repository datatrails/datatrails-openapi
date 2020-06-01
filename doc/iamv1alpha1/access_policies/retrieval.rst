
.. _iamv1alpha1access_policies_retrieval:

IAM Access Policies Retrieval (v1alpha1)
----------------------------------------

.. include:: ../../auth_url.rst

IAM access policy records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    access_policies/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the access_policy's identity you can fetch IAM access policy records using other
information you do know, such as the access_policy's name.


Fetch all IAM access_policies (v1alpha1)
========================================

To fetch all IAM access_policies records, simply GET the ``iam/access_policies`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/access_policies

Fetch specific IAM access Policy by identity (v1alpha1)
=======================================================

If you know the unique identity of the IAM access policy Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/access_policies/6a951b62-0a26-4c22-a886-1082297b063b

Fetch IAM Access Policies by name (v1alpha1)
============================================

To fetch all IAM access_policies with a specific name,  GET the ``iam/access_policies`` resource and filter on ``display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/access_policies?display_name=Acme


Each of these calls returns a list of matching IAM access_policies records in the form:

.. code-block:: JSON

    {
        "access_policies": [
            {
                "identity": "access_policies/6a951b62-0a26-4c22-a886-1082297b063b",
                "display_name": "Some description",
                "filters": "[
                    [\"location=basingstoke\", \"location=cambridge\"],
                    [\"asset_type=door_access_reader\"]
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
                        "behaviours": [ "behaviour1", "behaviour2" ],
                        "include_attributes": [ "attribute1", "attribute2" ]
                    }
                ]
            },
            {
                "identity": "access_policies/12345678-0a26-4c22-a886-1082297b063b",
                "display_name": "Some otherdescription",
                "filters": "[
                    [\"location=london\", \"location=oxford\"],
                    [\"asset_type=door_access_reader\"]
                ]",
                "access_permissions": [
                    {
                        "access_keys": [
                            {
                                "tessera": [ "key9", "key12" ],
                                "wallet": [ "key13", "key14" ]
                            },
                            {
                                "tessera": [ "key15", "key16" ],
                                "wallet": [ "key17", "key18" ]
                            }
                        ],
                        "behaviours": [ "behaviour3", "behaviour4" ],
                        "include_attributes": [ "attribute3", "attribute4" ]
                    }
                ]
            }
        ]
    }


.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

    A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1alpha1-iam-access_policies>`_
