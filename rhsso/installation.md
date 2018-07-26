## Guide
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#initial_setup

## Cluster Admin Requirements

- setting up imagetreams
- replacing templates
- image import 

This is the creation of resources in OpenShift might be possible to do with an opertor as long as the correct RBAC rules were in place.


## Manual setup steps
- keystore setup https://access.redhat.com/documentation/en-us/jboss_enterprise_application_platform/6.1/html-single/security_guide/index#Generate_a_SSL_Encryption_Key_and_Certificate

- recommended to deploy from the webconsole UI there are a lot of configuration options

- Example setup with keystore
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Example-Deploying-SSO

# Possible Actions

- Create ansible playbook to automate the process outlined here
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Example-Deploying-SSO

With possible prompts for overriding some of the values if needed. Although if it is for eval this may not be needed. We maybe able to just fill in defaults and generate passwords etc then output the result at the end of the install.

As other services need keycloak this should probably be the first thing we install we should then use this keycloak to configure the other services.

#Configuring Openshift to use keycloak as an identity provider

https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html/red_hat_single_sign-on_for_openshift/tutorials#OSE-SSO-AUTH-TUTE

```
- name: rh_sso
  challenge: false
  login: true
  mappingInfo: add
  provider:
    apiVersion: v1
    kind: OpenIDIdentityProvider
    clientID: openshift
    clientSecret: fa9d8e36-b914-47f1-be38-5739bed81434
    ca: xpaas.crt
    urls:
      authorize: https://sso-rhsso.cloudservices.skunkhenry.com/auth/realms/OpenShift/protocol/openid-connect/auth
      token: https://sso-rhsso.cloudservices.skunkhenry.com/auth/realms/OpenShift/protocol/openid-connect/token
      userInfo: https://sso-rhsso.cloudservices.skunkhenry.com/auth/realms/OpenShift/protocol/openid-connect/userinfo
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

# Other Notes

- In the cluster we setup the RHSSO 7.2 template was already present ( I assume it is part of our setup) but this template did not mention the keystore etc. Is this actually needed or can it just be done from the catalog without the need for creating a keystore as documented under
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Preparing-SSO-Authentication-for-OpenShift-Deployment ?