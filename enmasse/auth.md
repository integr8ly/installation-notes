# Auth

* A Keycloak instance is installed as part of the ansible installation of the enmasse operator. This Keycloak instance is what authenticates users for accessing Agents & Brokers.
* Agent & Broker pods are configured for auth via various `AUTHENTICATION_SERVICE_` env vars
* An OpenShift v3 Identify provider is configured in Keycloak, which uses an OAuth ServiceAccount i.e. If you have an OpenShift a/c, you can login to an enmasse console (via Keycloak).

## Questions
 - When we setup the OpenShift cluster to use RHSSO as an identity provider we could not login into the console using that user.
 (IE) we clicked on openshift, we clicked on rh_sso and put in the username password and got the following error
 
 ```
 {"error":"invalid_request","error_description":"Missing parameter: username"}
 ```
 
Flow : enmasse keycloak -> openshift -> cluster rhsso -> enmasse keycloak
