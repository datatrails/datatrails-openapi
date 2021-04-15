.. _azure-aad-assign-users:

Assign Users for Interactive Use
--------------------------------

To enable access for individual users to your Jitsuin Archivist:

#. Assign Users to the Jitsuin Archivist Enterprise application.
#. Grant assigned users the appropriate Jitsuin Archivist roles.

This Microsoft guide provides the general details for `assigning users`_ and
their roles.

.. _`assigning users`: https://docs.microsoft.com/bs-latn-ba/azure/active-directory/manage-apps/assign-user-or-group-access-portal

The key steps are as follows:

Locate your Jitsuin Archivist Enterprise Application
````````````````````````````````````````````````````

Having completed admin consent, locate the enterprise application principals
for your Jitsuin Archivist. There will be two **Homepage URLs** which match the
FQDN for the link you received. The URL for the root resource is your API
principal. This is where roles are assigned to users and non-interactive clients.
|userdocs_aad_enterprise_applications|

.. |userdocs_aad_enterprise_applications| image:: ../screenshots/userdocs_aad_enterprise_applications.png

.. note::
   The /webgate principal authorises your Jitsuin Archivist deployment to act
   on your users behalf. It needs no further configuration.

Select the principal with the Homepage URL matching your link.
|userdocs_aad_select_principal|

.. |userdocs_aad_select_principal| image:: ../screenshots/userdocs_aad_select_principal.png


Check that User assignment is required for your Jitsuin Archivist
`````````````````````````````````````````````````````````````````

The **User assignment required** setting must be **yes** in order to restrict
access to particular users in your directory. If it is set to **no** *any* user
at your organisation will be able to login.

|userdocs_aad_check_user_assignment|

.. |userdocs_aad_check_user_assignment| image:: ../screenshots/userdocs_aad_check_user_assignment.png

Add user to the enterprise application
``````````````````````````````````````
|userdocs_aad_add_user|

.. |userdocs_aad_add_user| image:: ../screenshots/userdocs_aad_add_user.png

Select the user for role assignment
```````````````````````````````````
|userdocs_aad_select_user|

.. |userdocs_aad_select_user| image:: ../screenshots/userdocs_aad_select_user.png
