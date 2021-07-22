
.. _compliance:

Compliance
----------

By maintaining a complete traceable record of When Who Did What to a Thing, RKVST makes it possible for any authorized stakeholder to quickly and easily verify that critical processes have been followed and recorded correctly.  And if they weren’t, the record makes it easy to discover where things went wrong and what to fix.

 

For instance: missed or late maintenance rounds can be detected simply by spotting gaps in the maintenance record; cyber vulnerable devices can be found by comparing ideal baselines with patching records; out-of-order process execution and handling violations are visible to all; and back-dating is automatically detectable.

 

All of this is very valuable in audit and RCA situations after an incident, where there is time to collect together Asset Records, piece together the important parts, and analyse the meaning. 



But what if the same information could be used for real-time decision-making that might avert an incident?

 

This is where RKVST’s “compliance posture” APIs come in. These take the thinking and processing burden off the client by providing a single, simple API call to answer the complex question: “given all you know about this asset, should I trust it right now?”. Additionally, and crucially for sensitive use cases, the yes or no answer comes with a detailed defensible reason why, which can be inspected by relevant stakeholders during or after the event.

 

When put all together, this enables high quality decision making based on the best available data, even giving confidence to automated or AI systems to play a full part in operations. Assets can be checked as part of access control logic, prior to accepting data or commands from them, prior to accepting a shipment, or anything else that is important to your business.


Creating Compliance Policies
----------------------------

Compliance Posture is measured against user-defined rule sets called Compliance Policies. Compliance policies are created once and then Assets can be tested against them at any point in time. For instance, a policy might state that “MaintenanceAlarm Events must be dealt with and a MaintenanceReport Event recorded with 72 hours”. This creates a Compliance Policy object in the system against which any asset can be tested as needed.

Types of Compliance Policies
----------------------------

RKVST allows users to define Compliance Policies of the following types:

COMPLIANCE_SINCE
^^^^^^^^^^^^^^^^

  This Compliance Policy checks if the time since the last occurence of a specific Event Type has elapsed a specified threshold. 
  For example "Time since last Maintenance must be less than 72 hours":

  .. code-block:: JSON

    {
        "compliance_type": "COMPLIANCE_SINCE",
        "description": "Maintenance should be performed every 72h",
        "display_name": "Regular Maintenance",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ]
        "event_display_type": "Maintenance Performed",
        "time_period_seconds": "259200"
    }

  .. note::
    event_display_type
      Type of event we want to check with this compliance policy

    time_period_seconds
      The maximum amount of time allowed since a specified event type last occurred in seconds


COMPLIANCE_CURRENT_OUTSTANDING
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  This Compliance Policy will only pass if there is an associated answering event addressing a specified outstanding event, for example defining pairs of Events like "Maintenance Request" and "Maintenance Performed".
  To correlate events define the attribute "arc_correlation_id" in the Event Attributes and set it to the same value on each pair of events that are to be associated.
  For example, checking there are no outstanding "Maintenance Request" Events that are not addressed by an associated "Maintenance Performed" Event:

  .. code-block:: JSON

    {
        "compliance_type": "COMPLIANCE_CURRENT_OUTSTANDING",
        "description": "There should be no outstanding Maintenance Requests",
        "display_name": "Outstanding Maintenance Requests",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ]
        "event_display_type": "Maintenance Requests",
        "closing_event_display_type":  "Maintenance Performed"
    }

  .. note::
    event_display_type
      Type of event that should be addressed by the event defined in closing_event_display_type

    closing_event_display_type
      Type of event addressing the event defined in event_display_type

COMPLIANCE_PERIOD_OUTSTANDING
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  This Compliance Policy will only pass if the time between a pair of correlated events did not exceed the defined threshold.
  To correlate events define the attribute "arc_correlation_id" in the Event Attributes and set it to the same value on each pair of events that are to be associated.
  For example, a policy checking that the time between "Maintenance Request" and  "Maintenance Performed" Events does not exceed the maximum 72 hours:

  .. code-block:: JSON

    {
        "compliance_type": "COMPLIANCE_PERIOD_OUTSTANDING",
        "description": "There should be no outstanding Maintenance Requests",
        "display_name": "Outstanding Maintenance Requests",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ]
        "event_display_type": "Maintenance Requests",
        "closing_event_display_type":  "Maintenance Performed",
        "time_period_seconds": "259200"
    }

  .. note::
    event_display_type
      Type of event that should be addressed by the event defined in closing_event_display_type

    closing_event_display_type
      Type of event addressing the event defined in event_display_type

    time_period_seconds
      Maximum amount of time that can elapse between associated events in seconds

COMPLIANCE_DYNAMIC_TOLERANCE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  This Compliance Policy will only pass if the time between a pair of correlated events did not exceed the defined variability.
  To correlate events define the attribute "arc_correlation_id" in the Event Attributes and set it to the same value on each pair of events that are to be associated.
  For example, a policy checking that the time between "Maintenance Request" and  "Maintenance Performed" Events in the last week does not exceed a variability
  of 0.5 standard deviations around the mean:

  .. code-block:: JSON

    {
        "compliance_type": "COMPLIANCE_DYNAMIC_TOLERANCE",
        "description": "Average time between Maintenance Requested/Performed"
        "display_name": "outlying Maintenance Requests",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ]
        "event_display_type": "Maintenance Requests",
        "closing_event_display_type": "Maintenance Performed",
        "dynamic_window": 604800,
        "dynamic_variability": 0.5
    }

  .. note::
    event_display_type
      Type of event that should be addressed by the event defined in closing_event_display_type

    closing_event_display_type
      Type of event addressing the event defined in event_display_type

    dynamic_window
      number of seconds in the past - only events in this time window are considered.

    dynamic variability
      exceeding this number of standard deviations from the mean will cause compliance to fail for a 
      particular pair of matching events..

COMPLIANCE_RICHNESS
^^^^^^^^^^^^^^^^^^^
      
  This Compliance Policy will only pass if the assertions conducted on an attribute value pass. An assertion is comprised of: an attribute name,
  a comparison value and an operator to compare with; for example "rad<7". The operator can be one of six relational operators:
  equal to, not equal to, greater than, less than, greater than or equal to, less than or equal to. [=|!=|>|<|>=|<=].
  Assertions are comprised of two lists, an inner list and outer list. The inner list states that, if any
  of the assertions pass, then the list is compliant (OR logic). For example: {"or": ["rad<7", "rad=10"]}. The outer list states that,
  all inner lists need to be compliant in order for the policy to be compliant (AND logic).

  Compliance is a signal, not a perfect answer. Therefore equivilence of floats is exact, not approximate.

  .. code-block:: JSON

    {
        "compliance_type": "COMPLIANCE_RICHNESS",
        "description": "Rad level is less than 7"
        "display_name": "Rad limit",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ],
        "richness_assertions": [
            { "or": ["rad<7"]}
        ],
    }

  .. note::
    richness_assertions
      The assertions to be made, against asset attributes, to check if the asset is compliant.

Compliance Policy Creation
--------------------------

.. include:: ../auth_url.rst

Create a Policy with:

  .. code-block:: shell
    
    $ curl -v -X POST \
        -H "@$BEARER_TOKEN_FILE" \
        -H "Content-type: application/json" \
        -d "@/path/to/jsonfile" \
        $URL/archivist/v1/compliance_policies

Using data from /path/to/jsonfile in the format described in #Types of Compliance Policies.

Sample response:

  .. code-block::  JSON

    {
        "identity": "compliance_policies/6a951b62-0a26-4c22-a886-1082297b063b",
        "compliance_type": "COMPLIANCE_CURRENT_OUTSTANDING",
        "description": "There should be no outstanding Maintenance Requests",
        "display_name": "Outstanding Maintenance Requests",
        "asset_filter": [
            { "or": ["attributes.arc_location_identity:locations/5eef2b71-35c1-4376-a166-6c64bfa72f4b"]}
        ]
        "event_display_type": "Maintenance Requests",
        "closing_event_display_type":  "Maintenance Performed",
        "time_period_seconds": "259200" 
    }

Compliance Checking
-------------------

The **compliancev1** endpoint reports on the status of an Asset's Compliance with Compliance Policies.

Query the endpoint:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/compliance/assets/6a951b62-0a26-4c22-a886-1082297b063b

or if determining compliance at some historical date:

.. code-block:: shell

    $ curl -v -X GET \
        -H "@$BEARER_TOKEN_FILE" \
        $URL/archivist/v1/compliance/assets/6a951b62-0a26-4c22-a886-1082297b063b?compliant_at=2019-11-27T14:44:19Z


The response is:

.. code-block:: JSON

    {
        "compliant": true,
        "compliance": [
            {
                "compliance_policy_identity": "compliance_policies/0000-0000-000000000-00000000",
                "compliant": true,
                "reason": ""
            }
        ],
        "compliant_at": "2019-11-27T14:44:19Z"
    }

.. note::
    compliant
        Overall compliance status, false if any Compliance Policy is not "compliant"

    compliant_at
        Timestamp at which compliance was determined

    The response contains a list of Compliance Statements.

        Each member of the list has the following attributes:

        compliance_policy_identity
            The identity of the Compliance Policy this statement refers to

        compliant
            Compliance status for this Compliance Policy

        reason
            description of non-compliance (only if compliant is false)


    See `Swagger GET API <openapi.html#get --archivist-v1-compliance>`_
