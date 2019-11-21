
.. _intro_lifecycle:

LifeCycle
---------

Jitsuin Archivist is an asset lifecycle assurance system. It helps enterprises 
keep on top of what is happening to their estate of connected devices and 
maintains a Full Service History for assets and Internet Things by keeping an 
immutable shared record of *When Who Did What to a Thing*. Following the 
principle that you can't secure what you can't see, this level of visibility 
and traceability is key to the security of Internet of Things installations. 

Jitsuin Archivist makes recording and auditing the full lifecycle of an asset 
simple: any authenticated participant (including an agent or endpoint on the 
device itself) can register the events they know about, and then all 
participants can see the aggregate picture of the asset's maintenance and 
operational history.  By knowing *When Who Did What to a Thing* human actors 
and connected systems can make stronger judgements about the trustworthiness 
of a device and the data it produces. 

Jitsuin Archivist Asset Records vs Digital Twins
================================================

Asset Records in Jitsuin Archivist are not Digital Twins, although they do 
share a number of useful characteristics. Understanding the differences will 
help to get the best out of the Archivist system.

+-------------------------------------------+-------------------------------------------+
| Digital Twin                              | Archivist Asset Record                    |
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

Jitsuin Archivist Asset Records and Digital Twins work well together to 
provide a full picture of Internet of Things operation: the Digital Twin 
offering a reliable and efficient view of the most recent known state of the 
device sensors, and Archivist providing an immutable record of its 
operational history and firmware state at the times of the those readings. 
The APIs in this SDK can be used to integraate Jitsuin Archivist with an IoT 
platform such as Microsoft Azure IoT Hub.

Asset Record Creation
=====================

The first event in an Asset Record's life is *creation*. This does not create 
the physcial device, but rather initializes its Full Service History record 
and begins tracking the device to which that record pertains. Devices must be 
registered in the Archivist system through the creation of an Asset Record 
before any other lifecycle events can be recorded and handled.  

Tracked vs Untracked assets
+++++++++++++++++++++++++++

Because the Full Service History of devices lasts forever it is not possible 
to actually create or delete assets from the system. Instead there is a 
concept of *tracked* assets (those that are interesting to the system and 
actively recording lifecycle events), and *untracked* assets (those that are 
no longer actively interesting, for example as a result of decommissioning). 

Untracked devices are still present in the system, and their Service 
Histories available, but they are removed from default lists and searches. 

This state is reflected in the ``tracked`` attribute. When an Asset Record is 
created its ``tracked`` attribute is automatically set to ``true``. 

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
``EvidenceLog`` event.

For more detail, see :ref:`asset_evidence`

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

Devices are marked as vulnerable through the ``vulnerabilityReport`` event, 
and are marked as patched through the ``firmwareUpdate`` event. 

To aid in analysis and compliance management these events can be linked by 
adding a common tag to the pair of messages: for example, a CVE reference.

For more detail, see :ref:`asset_vulnerability` and :ref:`asset_firmware`

Maintenance management
======================

There are many factors that affect the security and trustworthiness of a 
device beyond firmware bugs: expired digital IDs, access control failures, 
and physcial tampering among them. Jitsuin Archivist records and manages 
these events through the ``maintenanceRequest`` and ``maintenance`` event 
types. 

To aid in analysis and compliance management these events can be linked by 
adding a common tag to the pair of messages: for example, a work order number.

For more detail, see :ref:`asset_maintenance`

Asset Disposal
==============

When a real asset is disposed of for any reason it may be desirable to remove 
it from the Jitsuin Archivist system so that it does not appear in  
lists or searches. Because the Full Service History of devices lasts forever 
it is not possible to delete Asset Records from the system, but they can be 
removed from default lists and searches by setting the ``tracked`` property 
to ``false``.

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
and :ref:`asset_creation`


