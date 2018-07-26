## Guide
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#initial_setup

## Cluster Admin Requirements

- setting up imagetreams
- replacing templates
- image import 

This is the creation of resources in OpenShift might be possible to do with an opertor as long as the correct RBAC rules were in place.


## Manual setup steps
- keystore setup  before deployment https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Example-Deploying-SSO

- docs recommended to deploy from the webconsole UI.



# Possible Actions

- Create ansible playbook to automate the process outlined here
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Example-Deploying-SSO

With possible prompts for overriding some of the values if needed. Although if it is for eval this may not be needed. We maybe able to just fill in defaults and generate passwords etc then output the result at the end of the install.

As other services need keycloak this should probably be the first thing we install we should then use this keycloak to configure the other services.

#Configuring Openshift to use keycloak as an identity provider

https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html/red_hat_single_sign-on_for_openshift/tutorials#OSE-SSO-AUTH-TUTE


example master config to be added under identityProviders:

```
 - name: rh_sso
    challenge: false
    login: true
    mappingInfo: add
    provider:
      apiVersion: v1
      kind: OpenIDIdentityProvider
      clientID: openshift
      clientSecret: 14b201bd-70b7-46ba-ae36-2f84f0f6cec6
      ca: xpaas.crt
      urls:
        authorize: https://secure-sso-sso.cloudservices.skunkhenry.com/auth/realms/openshift/protocol/openid-connect/auth
        token: https://secure-sso-sso.cloudservices.skunkhenry.com/auth/realms/openshift/protocol/openid-connect/token
        userInfo: https://secure-sso-sso.cloudservices.skunkhenry.com/auth/realms/openshift/protocol/openid-connect/userinfo
      claims:
        id:
        - sub
        preferredUsername:
        - preferred_username
        name:
        - name
        email:
        - email

```      


It is important when generating the ketstores to make sure you pass in the correct hostname 

# Other Notes

- In the cluster we setup the RHSSO 7.2 template was already present ( I assume it is part of our setup) but this template did not mention the keystore etc. Is this actually needed or can it just be done from the catalog without the need for creating a keystore as documented under
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Preparing-SSO-Authentication-for-OpenShift-Deployment ?