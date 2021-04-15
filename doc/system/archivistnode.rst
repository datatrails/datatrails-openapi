
.. _archivistnode:

Archivistnode
-------------

.. include:: ../auth_url.rst

The **archivistnode** endpoint reports on the status of the blockchain.

Query the endpoint:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/archivistnode


The response is:

.. code-block:: JSON

    {
        "identity": "quorum",
        "blockchain_nodes": [
            {
                "validator_pubkey": {
                    "kty": "EC",
                    "crv": "P-256K",
                    "x": "VBKHictTWJC-3sqknXCb8MI4IxTc3c_My7lnem2C74E=",
                    "y": "ItNeb5d-6vEHkvtUOcDYrEADxsZXeOCJm18pQWntenE=",
                    "d": ""
                },
                "block_height": "38773",
                "connection_status": "REACHABLE"
                "genesis_hash":"0x1b526bd9c7f9bf7c43ba91ad07e5530eb7ceedf390396f9fbfeb68722e097e95",
                "state_root":"0x9606fc44a382938703678ac90581ab1260c9efd20ea8c7f90c87852bc982f3a7",
                "timestamp_committed": "2019-01-02T01:03:07Z",
                "timestamp_created": "2019-01-01T12:00:27Z",
                "syncing": null,
                "peers": [
                    {
                        "validator_pubkey": {
                            "kty": "EC",
                            "crv": "P-256K",
                            "x": "o0uZ8ix5DE42srPCw1o22wYibkHGkvyCuLVqwcVAxb0=",
                            "y": "W43sUjWg-ociR2x3CcAlWeOqc6oDkYui1JLup1q-ojU=",
                            "d": ""
                        },
                        "connection_status": "REACHABLE"
                    },
                    {
                        "validator_pubkey": {
                            "kty": "EC",
                            "crv": "P-256K",
                            "x": "5HcU1PJgTe0LGyGxKFrIPFZWdTbxPySfi6bKxdQeO8A=",
                            "y": "dEpMURyTwEGzpgIgLdm4Csl1BgF6H39tb1Kf8wLLhVI=",
                            "d": ""
                        },
                        "connection_status": "REACHABLE"
                    }
                ]
            }
        ]
    }

.. note::
    identity
        identifies the blockchain service.

    The response contains a list of blockchain identities and attributes.

    Each member of the list has the following attributes:

    validator_pubkey
        public key (ECDSA).

    block_height
        current no. of blocks in blockchain. May be zero if node is UNREACHABLE.

    connection_status
        - REACHABLE: node is reachable.
        - UNREACHABLE: node is currently unreachable.

    genesis_hash
        hash of the genesis block - use to verify that the blockchain is unchanged

    state_root
        state_root for the public state in the genesis block - use to verify that the blockchain is unchanged

    timestamp_committed
        timestamp (UTC) of latest block in the blockchain. May be zero (Jan 1st 1970) if node is UNREACHABLE.

    timestamp_created
        timestamp (UTC) of genesis block in blockchain.

    syncing
        if not null contains 3 integer fields, StartingBlock, CurrentBlock and HighestBlock indicating the
        the progress of syncing with the blockchain.

    peers
        list of peers.

    Each peer contains:

    validator_pubkey
        public key (ECDSA).

    connection_status
        - REACHABLE: blockchain is connected.
        - UNREACHABLE: peer is currently unreachable.

    See `Swagger GET API <openapi.html#get --archivist-v1-archivistnode>`_

