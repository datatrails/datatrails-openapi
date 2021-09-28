
.. _misc_paging:

API Request Paging
------------------

The varied endponts of the archivist API contain GET operations that
return a ``list`` of json records. This list size is restricted at
deployment of archivist (depending on the endpoint) to prevent buffer
and memory overflow.

If the user wishes to access all records of the endpoint then the page_size
parameter must be specified and the code must loop through repeated 
requests until no more records can be returned.

The first call to the endpoint specifies the page_size. The response body
may contain a field ``next_page_token``. If this is specified and non-empty repeated
calls to the endpoint specifying ``page_token=${next_page_token}`` are made until no
``next_page_token`` (or an empty value) is returned in the response.


CURL 
=====

Specify the required page_size on the first call to the endpoint and then the page_token
if specified in the response:

.. code-block:: shell

   RESPONSE=$( curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v2/assets?page_size=100)
   echo $RESPONSE | jq '.'  # send to stdout

   TOKEN=$( echo ${RESPONSE} | jq -r '.next_page_token' )

   while [ -n "${TOKEN}" ]
   do
       RESPONSE=$( curl -v -X GET \
            -H "@$BEARER_TOKEN_FILE" \
            $URL/archivist/v2/assets?page_token=${TOKEN})
       echo $RESPONSE | jq '.'  # send to stdout

       TOKEN=$( echo ${RESPONSE} | jq -r '.next_page_token' )

   done

Python 
======

Alternatively a better solution  is to use a ``python iterator``.
See the ``iterator``
method of the ``python`` class below.

.. code-block:: python

    """Archivist interface (python 3.6)
    """

    import json
    import logging
    from os import environ
    from os.path import sep as ospathsep
    import requests
    import urllib3
    

    class ArchivistException(Exception):
        """Indicate error
        """


    class Archivist:

        def __init__(self, url, auth, root="archivist", verify=True):
            self._baseurl = url
            self._auth = 'Bearer ' + auth.strip()
            self._auth_headers = {
                'content-type': 'application/json',
                'authorization': self._auth,
            }
            self._root = root
            self._verify = verify
    
        @property
        def auth_headers(self):
            return self._auth_headers
    
        @property
        def baseurl(self):
            return self._baseurl
    
        @property
        def root(self):
            return self._root
    
        @property
        def verify(self):
            return self._verify
    
        def query_path(self, target):
            query_path = ospathsep.join([self._baseurl, self._root, target])
            logging.debug(query_path)
            return query_path
    
        def get(self, target):
    
            response = requests.get(
                self.query_path(target),
                headers=self._auth_headers,
                verify=self._verify,
            )
    
            logging.debug(response)
    
            return response
    
        def asset(self, asset_id):
            """Returns asset
    
            asset_id: asset identity
            """
            response = self.get(f"v2/{asset_id}")
            if response.status_code != 200:
                raise ArchivistException(f"Response code is {response.status_code}")
    
            return response.json()
    
        def post(self, target, request):
    
            response = requests.post(
                self.query_path(target),
                data=json.dumps(request),
                headers=self._auth_headers,
                verify=self._verify,
            )
    
            logging.debug(response)
    
            return response
    
        def iterator(self, path, field, page_size=None, query_params=""):
            """Returns iterator that lists objects
    
            path: REST path e.g. v2/assets
            query_params: REST query string - must begin with &

            If page size is specified return the list of records in batches of page_size
            until next_page_token in response is null.

            If page size is unspecified return up to the internal limit of records.
            (different for each endpoint)
            """
            
            paging = ""
            if page_size is not None:
                paging = f"page_size={page_size}"

            while True:
                response = self.get(f"{path}?{paging}{query_params}")
                logging.debug(response)
    
                if response.status_code != 200:
                    raise ArchivistException(f"Response code is {response.status_code}")
    
                data = response.json()
                try:
                    records = data[field]
                except KeyError:
                    raise ArchivistException(f"No {field} found")
    
                for record in records:
                    yield record
    
                token = data.get("next_page_token")
                if not token:
                    break
    
                paging = f"page_token={token}"
    
        def assets(self, page_size=None, query_params=None):
            """Returns iterator that lists assets
    
            query_params: REST query string
            """
            return self.iterator(
                "v2/assets",
                "assets",
                page_size=page_size,
                query_params,
			)
    
        def events(self, page_size=None, query_params=None):
            """Returns iterator that lists events
    
            query_params: REST query string
            """
            return self.iterator(
                "v2/assets/-/events",
                "events",
                page_size=page_size,
                query_params,
            )

        def blockchain(self, identity, page_size=None):
            """Returns iterator that lists blockchain transactions
    
            identity: asset/event identity
            """
            return self.iterator(
                f"vialpha1/blockchain/{identity}",
                "transactions",
                page_size=page_size,
            )


and typical usage may look like this:

.. code-block:: python

    # Initialise connection to Archivist
    archivist = Archivist(archivist_url, authtoken)
    if archivist is None:
        raise SystemExit

    no_of_events = 0
    for event in archivist.events(
            page_size=10,
            query_params="confirmation_status=CONFIRMED",
    ):
        no_of_events += 1
        print("event", event)

    no_of_transactions = 0
    for transaction in archivist.blockchain(
            "assets/add30235-1424-4fda-840a-d5ef82c4c96f/events/11bf5b37-e0b8-42e0-8dcf-dc8c4aefc000",
            page_size=10,
    ):
        no_of_transactions += 1
        print("transaction", transaction)

