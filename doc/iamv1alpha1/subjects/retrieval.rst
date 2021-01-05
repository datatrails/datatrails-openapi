
.. _iamv1alpha1subjects_retrieval:

IAM Subjects Retrieval (v1alpha1)
---------------------------------

.. include:: ../../auth_url.rst

IAM subject records in Jitsuin Archivist are tokenized at creation time and referred
to in all API calls and smart contracts throughout the system by a unique
identity of the form:

::

    subjects/12345678-90ab-cdef-1234-567890abcdef.

If you do not know the subjects's identity you can fetch IAM subject records using other
information you do know, such as the subject's name.


Fetch all IAM subjects (v1alpha1)
=================================

To fetch all IAM subjects records, simply GET the ``iam/subjects`` resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/subjects

Fetch specific IAM Subject by identity (v1alpha1)
=================================================

If you know the unique identity of the IAM subject Record simply GET the
resource:

.. code-block:: shell

   $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/subjects/6a951b62-0a26-4c22-a886-1082297b063b

Fetch IAM Subjects by name (v1alpha1)
=====================================

To fetch all IAM subjects with a specific name,  GET the ``iam/subjects`` resource and filter on ``display_name``:

.. code-block:: shell

   $ curl -g -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1alpha1/iam/subjects?display_name=Acme


Each of these calls returns a list of matching IAM subjects records in the form:

.. code-block:: JSON

    {
        "subjects": [
            {
                "identity": "subjects/6a951b62-0a26-4c22-a886-1082297b063b",
                "display_name": "Some description",
                "wallet_pub_key": ["key1"],
                "wallet_address": ["address1"],
                "tessera_pub_key": ["key2"]
            },
            {
                "identity": "subjects/12345678-0a26-4c22-a886-1082297b063b",
                "display_name": "Some otherdescription",
                "wallet_pub_key": ["key5"],
                "wallet_address": ["address5"],
                "tessera_pub_key": ["key7"]
            }
        ]
    }

.. note::

    The number of records returned has a maximum limit. If this limit is too small then one must use 
    :ref:`misc_paging`.

.. note::

   The total number of subjects that exist is returned in the response header field 'x-total-count' if
   the 'x-request-total-count' header on the request is set to 'true'.
   The curl option '-i' will emit this to stdout.

.. note::

   A full API reference is available in `Swagger GET API <openapi.html#get--archivist-v1alpha1-iam-subjects>`_
