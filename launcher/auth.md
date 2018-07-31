# Auth

* Launcher installs without any auth by default. This prevents launcher from auto-creating resources in the openshift cluster (It is left to the developer to download the launcher project locally and create resources in openshift/minishift)
* Launcher expects a Github App/Client to be created and configured (client id & token). There are parameters in the launcher template for this. This is used to create repos in the users Github account when they choose a launch mission.
* Launcher can be configured to use keycloak for authentication, and allow users to authorize launcher access to their openshift account. When configured correctly, launcher can auto-create the launch mission resources in a specified namespace in openshift


## Client & Identity Provider setup with 2 Keycloaks

This setup has a keycloak instance used by OpenShift for identity (OS Keycloak), and another keycloak instance used by Launcher (Launcher Keycloak).

* Users are managed centrally in OS Keycloak
* An 'openid-connect' Client is created in the OS Keycloak. A 'keycloak-oidc' Identity Provider is created in the Launcher Keycloak to use this Client. Also, a Client is created in the Launcher Keycloak. This allows OpenShift users to login to Launcher (a user is created in Launcher Keycloak after login, and linked to the OpenShift user)
* In the Launcher flow, the user can 'Authorize' Launcher to create resources in OpenShift. This uses the same Client in Launcher Keycloak, but a different Identity Provider. An 'openshift-v3' Identity Provider is used, which expects an OAuthClient to be created in OpenShift. After Authorizing, another Identity Provider link is created for the user.
* Again in the Launcher flow, the user can 'Authorize' Launcher to create repos in the users Github account. This uses a Client in Github, and another Identity Provider in Launcher Keycloak ('github' provider).