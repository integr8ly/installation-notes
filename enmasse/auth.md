# Auth

* A Keycloak instance is installed as part of the ansible installation of the enmasse operator. This Keycloak instance is what authenticates users for accessing Agents & Brokers.
* Agent & Broker pods are configured for auth via various `AUTHENTICATION_SERVICE_` env vars
* An OpenShift v3 Identify provider is configured in Keycloak, which uses an OAuth ServiceAccount i.e. If you have an OpenShift a/c, you can login to an enmasse console (via Keycloak).
* set of custom plugins installed that handle amqp client authentication
*  The user that can access the console has to be the same user that provisioned the piece of enmasse as there is a link created between the openshift user and a user in the enmaase keycloak

## Options

Configure the Enmaase keycloak to use the cluster keycloak as an identity provider

## Questions

 
Flow : enmasse keycloak -> openshift -> rhsso -> enmasse keycloak
