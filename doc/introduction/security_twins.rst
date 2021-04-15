
.. _intro_security_twins:

Compliance Policies
-------------------

In order to make these trust decisions, Jitsuin Archivist can be configured
with *Compliance Policies* to check assets against. These policies specify
things like tolerance for vulnerability windows, or SLAs for open maintenance
calls. For example:

    "Assets must be patched within 40 days of vulnerability notification"

    "Maintenance calls must be answered within 72 hours"

Individual assets either pass or fail, and organizations can calculate
their overall security/compliance posture based on what proportion of their
assets are breaching their policy set.

Compliance signals can also be used to identify where risk lies in an
organization and help to prioritize remedial activities.

User-defined Compliance Policies
++++++++++++++++++++++++++++++++

.. note ::
    User-defined compliance policies are currently not supported.
    Future versions of Jitsuin Archivist will allow users to create
    policies that are best tuned to their business needs


Built-in Compliance Policies
++++++++++++++++++++++++++++

Every Jitsuin Archivist implements a default policy in
``compliance_policies/0000-0000-000000000-00000000`` which checks for
outstanding firmware vulnerabilities or maintenance requests. If any
requests are outstanding then the asset fails compliance. If all reported
vulnerabilities have been patched and maintenance requests serviced then
it passes.


For further details on the API for compliance posture, see :ref:`compliance`. 
