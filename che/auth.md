# Auth

* The templates in the che repo (https://github.com/eclipse/che) include a [DeploymentConfig for Keycloak](https://github.com/eclipse/che/blob/master/deploy/openshift/templates/multi/keycloak-template.yaml)
* The che-server is configured to use this Keycloak instance via the `CHE_KEYCLOAK_AUTH__SERVER__URL` [env var](https://github.com/eclipse/che/blob/3dff9f09fddd9cd0580f455bbe94ff480210dce8/deploy/openshift/templates/che-server-template.yaml#L116-L117)
  * defaults to `${PROTOCOL}://keycloak-${NAMESPACE}.${ROUTING_SUFFIX}/auth`
* It is also possible to set what Realm & Client to use with env vars (but these don't need to be set by default)
  * `CHE_KEYCLOAK_REALM=che`
  * `CHE_KEYCLOAK_CLIENT__ID=che-public`
* More info on using your own Keycloak instance here https://www.eclipse.org/che/docs/openshift-config.html#multi-user-using-own-keycloak-and-psql
* Keycloak can be configured (manually) to do User Federation (e.g. LDAP) or Social Login & Brokering if needed, but the default keycloak instance has no Federation or Brokering.
  * https://www.eclipse.org/che/docs/user-management.html
* A ServiceAccount OAuthClient is *NOT* used by che

# Github Integration

Che has the ability to integrate with Github, providing 2 main features:

* Import a git repo as a Che Project (shows a list of user's repos)
* Do version control from the Che IDE

There are 2 ways to configure Che server for Github integration.

* Set env vars in Che server for a github client id & secret (embedded/single user mode)
* Defer to a Github Identity Provider in Keycloak (delegated/multi user mode)

More info here https://www.eclipse.org/che/docs/user-management.html#social-login-and-brokering