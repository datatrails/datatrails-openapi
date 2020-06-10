
.. _intro_policies:

Access Policies
---------------

Sharing the right amount of information with your Value Chain partners is
critical to creating a trustworthy Shared Service History for assets. It
is important that every participant be able to see and contribute to the
management of assets they have shared responsibility for without compromising
security, commercial, or private personal information.

For example, competing vendors should not see each other's information, but
both should be able to freely collaborate with their mutual customer or
industry regulator.

In other scenarios, it is desirable to share basic maintenance information
with a vendor or external maintenance company, whilst keeping critical
operating information such as run cycles and cyber SLAs within a much smaller
group.

Access Policies are the method through which this access is defined, allowing
asset owners to collaborate with just the right partners at the right time,
sharing as much or as little access to Shared Service Histories as the
needs of the value chain partners dictate.

.. note ::
    To collaborate with a value chain partner you first need to exchange
    public keys in an out-of-band process such as email, and import the
    partner's keys into your system as an IAM Subject.

Configuring Access Policies
===========================

When To Create An Access Policy
+++++++++++++++++++++++++++++++

All transactions are private by default, meaning that only the asset owner can
see and update asset Service Histories until a sharing policy has been set up.
This ensures ready compliance with important regimes such as GDPR and antitrust
regulations, as well as allowing safe and ready collaboration with a large and
diverse range of value chain partners in the Jitsuin network when required. 

This means that Access Policies must be defined as soon as a need is identified
in order to facilitate collaboration between value chain partners.

Considerations
++++++++++++++

As with any system handling large amounts of important data, it is important
to carefully consider the design and scope of your access policy rules.

Every situation is different, and the Jitsuin Archivist Access Policy system
is flexible and powerful enough to support most situations, but in general
it is recommended to follow some basic rules:

* Aim for fewest possible number of policies: This makes it much easier to
  review and manage access rights. 
* Balance complex, highly-specific policies with simple, broad ones: Rights
  granted by policy are additive.
* A single Access Policy can contain several Permission Groups, so it is
  possible to define a single filter to cover a particular population of
  assets, then apply different rights to different Subjects. This is often
  a simpler way to manage access than to create separate Access Policies for
  each set of Subjects.
* Remember attributes can change: ABAC policies are applied at time of access
  request, not at time of creation, so changing attributes on an asset may
  change which access policies apply to it. This is one of the primary
  advantages to an ABAC system but still needs to be borne in mind when
  designing access control processes.

Revoking Access
+++++++++++++++

Jitsuin Archivist adopts a 'default deny' approach so access to an Asset
Record is only possible if an Access Policy explicitly allows it.

Revoking access can therefore be achieved in a number of ways, any of which
may be more or less appropriate for the circumstances:

* Remove the whole Access Policy
* Change the attributes of the Asset so that it no longer matches the Access
  Policy (eg change location)
* Change the attributes of the user or Subject so that they no longer match
  the Access Policy (eg change IDP group)
* Turn off the user's login at the IDP

Policy Definition
=================

Jitsuin Archivist employs a principle called `Attribute-Based Access Control
<https://en.wikipedia.org/wiki/Attribute-based_access_control>`_.

Rather than applying a specific policy to each asset, or grouping them into
rigid hierarchies, policies are defined in terms of the observable properties
(or *attributes*) of assets and users, and if both match, the policy is
applied. This enables much greater flexibility and expressivity than
traditional hierarchical or role-based methods, whilst at the same time
reducing complexity in handling large-scale systems.

Archivist Access Policies comprise 4 main parts:

- *Attribute Filters* and *Subjects*, which determine which users and
  assets the policy will apply to; and
- *Behaviours* and *Share Attributes*, which specify the read and write
  access granted to Archivist Asset Records under this policy

Attribute Filters
+++++++++++++++++

*Attribute Filters* are a set of attributes to test against asset attributes.
This policy will apply to all assets that match. The filters take the
form of a list of lists, where at least one attribute in each list must match
the asset attributes. Or in other words, inner lists are OR, while outer lists
are AND. For example:

::

  Filters = [
    [ListOne, ...],
    [ListTwo, ...],
    [ListThree, ...]
  ]

In the above simplified example, the policy will apply to an asset only if the
asset's attributes match *at least one* entry from each of ListOne *AND* ListTwo
*AND* ListThree.

In more detail:

::

  Filters = [
    [type=Pump, type=Valve],
    [vendor=SynsationIndustries],
    [location=ChicagoWest,location=ChicagoEast]
  ]

In this case, the policy would apply to any Pump or Valve from
SynsationIndustries installed in the ChicagoWest or ChicagoEast sites.
It would not match:

* Other device types from SynsationIndustries;
* Pumps or Valves from any other vendor;
* SynsationIndustries Valves installed in a different location

Subjects
++++++++

*Subjects* specify which users or value chain partners will be granted the
policy access rights. These must have been imported as IAM Subjects before
creating the policy.

.. note ::

    In future releases of Archivist it will be possible to specify qualifying
    Access Subjects by attribute. Presently each individual Subject must be included
    in the policy.

Behaviours
++++++++++

*Behaviours* specifies which asset behaviours the *Subjects* will be
allowed to use. This can be considered equivalent to *write access*

.. note ::

    See :ref:`intro_behaviours` for details of behaviours.

    An organization's ability to contribute to the Shared Service History 
    for a given asset will be the union of all *Behaviours* write access granted
    under all policies.

Share Attributes
++++++++++++++++
 
*Share Attributes* specify which attributes of the asset will be made visible
to the specified *Subjects*. This can be considered equivalent to *read access*.

.. note ::

    See :ref:`intro_behaviours` for details of system-reserved ``arc_*``
    attributes which should generally be shared with all Subjects.

    An organization's copy of the Shared Service History for a given asset
    will contain the union of all *Share Attributes* read access granted under
    all policies.

