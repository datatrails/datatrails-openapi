
.. _intro_lifecycle:

LifeCycle
---------

Jitsuin Archivist is an asset lifecycle assurance system built to lower 
business risk. It enables enterprises to reveal, reduce and report risks
introduced through connected devices and Digital Transformation. Jitsuin
Archivist maintains a Full Service History for assets and Internet Things
by keeping a permanent shared record of *When Who Did What to a Thing*. 
Following the principle that you can't secure what you can't see, this level
of visibility and traceability is key to lowering the risk of business
transformation with the Internet of Things. 

Jitsuin Archivist makes recording and auditing the full lifecycle of an asset 
simple: any authorized participant (including an agent or endpoint on the 
device itself) can register the events they know about, from which all 
participants can see a relevant aggregate picture of the asset's maintenance
and operational history.  By knowing *When Who Did What to a Thing* human
actors and connected systems can make stronger judgments about the
trustworthiness of a device and the data it produces. 

Security Twins (Jitsuin Archivist Asset Records) vs Digital Twins
=================================================================

A Digital Twin simplifies Digital Transformation by representing real-world
objects in virtual form that allows business applications to connect to
Internet Thing data through simple APIs without stressing the
power-constrained devices and unreliable network connectivity that often go
hand-in-hand with IoT installations.  

Security Twins - built from Asset Records in Jitsuin Archivist - are not
Digital Twins, although they do share a number of useful characteristics.
Security Twins provide a trust layer that underpins the trustworthiness of
Digital Twin applications. Understanding the differences between the two
will help to get the best out of the Archivist system and your Digital
Transformation.

+-------------------------------------------+-------------------------------------------+
| Digital Twin                              | Security Twin                             |
+===========================================+===========================================+
| | Typically connected to an agent on the  | | Doesn't rely on a direct connection to  |  
| | physical twin via real-time interfaces  | | the physical twin. Any authenticated    |
| |                                         | | actor may report on asset state         |
+-------------------------------------------+-------------------------------------------+
| | Typically seeks to model sensor state   | | Concentrates on operational and         |
| | and 'hot data' from the device          | | maintenance state of the device. Sensor |
| |                                         | | data is typically only reported if it   |
| |                                         | | is out of safe range or compliance      |
+-------------------------------------------+-------------------------------------------+
| | Acts as a proxy for collecting          | | Acts as a Full Service History for the  |
| | any reading from the device when a      | | device and its maintenance operations   |
| | direct connection is not feasible       | |                                         |
+-------------------------------------------+-------------------------------------------+
| | Acts as an endpoint for business        | | Provides the necessary information and  |
| | applications to gather data or receive  | | insight from the asset history and      |
| | commands                                | | status to augment Digital Twin data     |
| |                                         | | with a score of trustworthiness,        |
| |                                         | | provenance and compliance               |
+-------------------------------------------+-------------------------------------------+

Security Twins and Digital Twins work well together to provide a full picture
of Internet of Things operation: the Digital Twin offering a reliable and
efficient view of the most recent known state of the device sensors; and
the Security Twin (Archivist) providing an immutable record of its operational
history and firmware state at the times of the those readings. 
The APIs in this SDK can be used to integrate Jitsuin Archivist with an IoT 
platform such as Microsoft Azure IoT Hub, thereby bringing the power of a
Security Twin layer without disrupting telemetry and data operations.

Asset Record Creation
=====================

The first event in an Asset Record's life is *creation*. This initializes its
Full Service History record and begins tracking the device to which that
record pertains. Devices must be registered in the Archivist system through
the creation of an Asset Record before any other lifecycle events can be
recorded and handled.  

Tracked vs Untracked assets
+++++++++++++++++++++++++++

Because the Full Service History of devices lasts forever it is not possible 
to actually delete Asset Records from the system. Instead there is a 
concept of *tracked* assets (those that are interesting to the system and 
actively recording lifecycle events), and *untracked* assets (those that are 
no longer actively interesting, for example as a result of decommissioning). 

Untracked devices are still present in the system, and their Service 
Histories available, but they are removed from default lists and searches. 

This state is reflected in the ``tracked`` attribute. When an Asset Record is 
created its ``tracked`` attribute is automatically set to ``TRACKED``. 

Asset modification
==================

Asset attributes can be modified after creation by using the API. 
Only the asset identity is fixed: all other attributes can be modified.

Modification of significant attributes (such as firmware version) results 
in an audited entry in the asset history.

Recording events in the asset lifecycle
=======================================

Any interaction with a device can be significant: from user logins to
unexpected restarts or ad-hoc observations. Keeping a record of these
events can build up a picture of how an asset came to be in its current
state and provide crucial insight to future maintenance staff, auditors,
and security remediation teams.

Archivist allows recording these general lifecycle events through the
``RecordEvidence`` behaviour.

For more detail, see :ref:`recordevidence_behaviour`

Firmware security management
============================

One of the most common sources of security breach in connected systems is 
unpatched software in devices. By providing a common platform for all 
relevant participants to collaborate on device maintenance, Jitsuin 
Archivist simplifies effective vulnerability disclosure, device recalls, 
regulatory compliance, and improved decision making.

As well as recording the current firmware version of each device in its 
Asset Record, a full history of prior versions, vulnerability warnings, 
patches, and times left unpatched is maintained.  

Handling the firmware lifecycle record of an asset is performed through
the Firmware behaviour. Devices can be marked as requiring an update for
any reason using the ``updateRequired`` operation, are marked as vulnerable
through the ``vulnerability`` operation, and record successful patching
through the ``update`` operation.

To aid in analysis and compliance management these events can be linked by 
adding a common tag to the pair of messages in the ``arc_correlation_value``
attribute.

For more detail, see :ref:`firmware_behaviour`

Maintenance management
======================

There are many factors that affect the security and trustworthiness of a 
device beyond firmware bugs: expired digital IDs, access control failures, 
and physical tampering among them. Jitsuin Archivist records and manages 
these events through the ``maintenanceRequest`` and ``maintenance`` event 
types. 

To aid in analysis and compliance management these events can be linked by 
adding a common tag to the pair of messages: for example, a work order number.

For more detail, see :ref:`maintenance_behaviour`

Asset Disposal
==============

When a real asset is disposed of for any reason it may be desirable to remove 
it from the Jitsuin Archivist system so that it does not appear in  
lists or searches. Because the Full Service History of devices lasts forever 
it is not possible to delete Asset Records from the system, but they can be 
removed from default lists and searches by setting the ``tracked`` property 
to ``UNTRACKED``.

How to create an Asset Record
=============================

Creating an Asset Record with the APIs is fast and straightforward. 
Follow the steps in this order for best success:

1. Determine if the asset is associated with a particular location. 
If it is, look up the location identity (if it already exists) or get a 
new location identity by creating one.

2. Import any attachments associated with the asset (for example, 
photograph of the physical unit) and get their identities.

3. Create the Asset, including the (optional) identities of the location 
and attachments.

For more detail, see :ref:`locations_creation`, :ref:`attachments_upload` 
and :ref:`assetv2_creation`

Understanding asset lifecycle events
====================================

For details of how to retrieve Asset Records from the system see
:ref:`assetv2_retrieval`.

Lifecycle events in the Archivist system give stakeholders a shared view
of "When Who did What to a Thing".  The "What" and the "Thing" are quite
straightforward, but the "When" and "Who" can be more nuanced.

Timestamps
++++++++++

Once committed to the Jitsuin Archivist system, each lifecycle event record
carries 3 separate timestamps:

* ``timestamp_declared`` - an optional user-supplied value that tells when
  an event happened. This is useful for cases where the client system is
  off-line for a period but the user still wishes to record the accurate
  time and order of activities (eg inspection rounds in an air-gapped
  facility).
  If unspecified, the system sets ``timestamp_declared`` equal to 
  ``timestamp_accepted`` (see below).
* ``timestamp_accepted`` - the time the event was actually received on the
  Jitsuin Archivist node's REST interface. Set by the system, cannot be
  changed by the client.
* ``timestamp_committed`` - the time the event was confirmed distributed to
  all DLT nodes in the value chain.  Set by the system, cannot be changed
  by the client.

Having these 3 fields enables users of Jitsuin Archivist to accurately reflect
what is claimed, whilst also preventing tampering and backdating of entries.

User principals
+++++++++++++++

Once committed to the Jitsuin Archivist system, each lifecycle event record
carries 2 separate user identities:

* ``principal_declared`` - an optional user-supplied value that tells who
  performed an event. This is useful for cases where the user principal/
  credential used to connect to the Archivist system does not accurately or
  usefully reflect the real-world agent (eg a multi-user application with 
  device-based credentials).
* ``principal_accepted`` - the actual user principal information belonging
  to the credential used to access the Jitsuin Archivist node's REST interface.
  Set by the system and retrieved from the authorizing IDP, cannot be changed
  by the client.
