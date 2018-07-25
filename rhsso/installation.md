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

# Other Notes

- In the cluster we setup the RHSSO 7.2 template was already present ( I assume it is part of our setup) but this template did not mention the keystore etc. Is this actually needed or can it just be done from the catalog without the need for creating a keystore as documented under
https://access.redhat.com/documentation/en-us/red_hat_jboss_middleware_for_openshift/3/html-single/red_hat_single_sign-on_for_openshift/index#Preparing-SSO-Authentication-for-OpenShift-Deployment ?