.. _intro_behaviours:

Behaviours
----------

Jitsuin Archivist supports a wide range of cyber-physical assets with
very different capabilities and properties: some will have simple
firmware maintenance lifecycles; others may have complex software
configurations to manage; and yet others may have significant physical
maintenance requirements to meet.

'Behaviours' are the technical mechanism through which Asset Records
(and by extension estate security and compliance posture) are managed.
Behaviours represent aspects of the asset lifecycle such as firmware
updates or physical maintenance.

Within each behaviour there is a set of 'operations' which update the
asset's service history and create the basis for the shared evidence
base for compliance insights, patch performance and so on.

Declaring allowed Behaviours
============================

In order to maintain integrity of assets' service histories and the overall
security and compliance posture of an estate it is necessary to restrict
which behaviours are pertinent to each asset, and therefore what statements
can be made about the asset's lifecycle. It is therefore necessary to
supply a list of allowed behaviours when first creating the Asset Record.

System-defined attributes
=========================

Certain asset attributes are manipulated and interpreted by the system
in order to provide compliance and security insights for the asset.  In
order to get the best benefit from the Archivist it is essential to 
take care to handle these properties carefully and consistently when
passing them to behaviours operations.

All asset properties with an ``arc_`` prefix are used for system-defined
purposes. Most operations also support custom properties which can have
arbitrary names, though it is recommended to adopt a naming scheme which 
minimizes chances of collisions or confusion with other clients in the 
value chain.




