
.. _bearer-token:

Authorization and Authentication
--------------------------------

The authorization and authentication is handled by generated bearer tokens.
The bearer token should be stored in a file and an environment variable **BEARER_TOKEN_FILE**
contains the name of the file.

The text in the BEARER_TOKEN_FILE should follow the format:

.. code-block:: text

    Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

where the x's are replaced by the actual contents of the bearer token.

.. note::

    Recommended that the directory containing the **BEARER_TOKEN_FILE** have 0600 permissions


.. todo:: Update when machine authentication methodology has been defined

