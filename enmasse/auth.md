# Auth

* A Keycloak instance is installed as part of the ansible installation of the enmasse operator. This Keycloak instance is what authenticates users for accessing Agents & Brokers.
* Agent & Broker pods are configured for auth via various `AUTHENTICATION_SERVICE_` env vars
* An OpenShift v3 Identify provider is configured in Keycloak, which uses an OAuth ServiceAccount i.e. If you have an OpenShift a/c, you can login to an enmasse console (via Keycloak).