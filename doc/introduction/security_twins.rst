
.. _intro_security_twins:

Security Twins and Trustworthiness
----------------------------------

Trust is subjective. Compliance policies are a judgement call. No matter what
security technology you have in play every trust decision you make will depend
on the circumstances: who is accessing what; where they're coming from; how
sensitive an operation they're attempting; the consequences of getting it
wrong. An asset that is safe in one context may not be in another.

Difficult decisions are slow to be made, and slow decisions means lost time.
No matter what security mechanisms are in place, if you can't *trust* the
assets and data in your systems then the chances are you won't be able to
automate decisions and processes, keeping humans in the loop and losing the
scale advantages of AI and IoT.

Security Twins take the heavy lifting out of this process by providing a
simple trust layer that any client or process can ask. They answer the
question: given all that I know about this asset - its security status, 
maintenance history, active alarms - can I trust it with what I'm trying
to do right now? They help you make smarter, faster, better decisions
*and* provide traceability that enable you to explain those decisions
later on.


Compliance policies
===================

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
