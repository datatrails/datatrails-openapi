
.. _intro_attachments:

Attachments
-----------

Attachments in Jitsuin Archivist enable images, PDFs and other binary data 
to be attached to assets and events.  This brings added richness to the 
evidence base and facilitates high fidelity collaboration between 
stakeholders.

Uploading an Attachment
=======================

The first step is to upload the attachment to the attachments API and noting
the uuid of the uploaded attachment. See :ref:`blobsv1_upload`

Attachments on assets
=====================

Adding an attachment to an asset enables recording of characteristics of 
the asset that are very difficult to capture in text.  For example, the 
specific placement of a component or the device's serial number or rating 
plate.

While asset attachments are generally expected to be unique, the same 
attachment can be applied to multiple assets, such as a stock image of a 
type of device.

See :ref:`attachments_behaviour_attach`

The asset 'arc_primary_image'
++++++++++++++++++++++++++++++++++++++

Attachments to assets are named in their ``arc_display_name`` property, so 
that they can be searched and indexed.  Names are arbitrary and may be 
defined according to the needs of the application, but one name is 
reserved and interpreted by the Jitsuin stack: ``arc_primary_image``.  

If an asset has an attachment named ``arc_primary_image`` then this will be 
used by the user interface and other Jitsuin tools to represent the asset. 

Attachments on events
=====================

Adding an attachment to an event allows recording and communication of
asset status that is difficult to capture in text.  For example:

* a photograph of physical state of a device such as alignment of
  components or wear on tamper seals at the time of a particular
  inspection.
* a PDF of a safety conformance report to support a maintenance event.
* a software manifest to support an update.
* an x-ray image

To add attachments to an event simply specify an ``attachments`` list 
in the ``attributes`` of the ``request`` block when posting an event.
See :ref:`attachments_behaviour_attach` for an example of the JSON layout.

