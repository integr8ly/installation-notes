
## Eclpise Che: Manual install on OpenShift

Follow the 'OpenShift Container Platform HTTP Setup' from https://www.eclipse.org/che/docs/openshift-multi-user.html#openshift-container-platform

```
$ oc login https://cloudservices.skunkhenry.com:8443 --token=CZGpw-kIXLThhv8kB69GK6gPYniIL5cIb-ACrQzSTp4
The server uses a certificate signed by an unknown authority.
You can bypass the certificate check, but any data you send to the server could be intercepted by others.
Use insecure connections? (y/n): y

Logged into "https://cloudservices.skunkhenry.com:8443" as "admin" using the token provided.

You have access to the following projects and can switch between them with 'oc project <projectname>':

  * default
    kube-public
    kube-service-catalog
    kube-system
    logging
    management-infra
    openshift
    openshift-ansible-service-broker
    openshift-infra
    openshift-node
    openshift-template-service-broker
    openshift-web-console
    test

Using project "default".

$ export ROUTING_SUFFIX=cloudservices.skunkhenry.com
$ oc new-project che
Now using project "che" on server "https://cloudservices.skunkhenry.com:8443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git

to build a new example application in Ruby.
$ oc new-app -f multi/postgres-template.yaml
--> Deploying template "che/postgres" for "multi/postgres-template.yaml" to project che

     postgres
     ---------
     Che

     * With parameters:
        * Eclipse Che version=nightly
        * Postgres DB Image=docker.io/eclipse/che-postgres

--> Creating resources ...
    deploymentconfig "postgres" created
    service "postgres" created
    persistentvolumeclaim "postgres-data" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose svc/postgres' 
    Run 'oc status' to view your app.
$ oc new-app -f multi/keycloak-template.yaml -p ROUTING_SUFFIX=${ROUTING_SUFFIX}
--> Deploying template "che/keycloak" for "multi/keycloak-template.yaml" to project che

     keycloak
     ---------
     Che

     * With parameters:
        * htpps or http protocol=http
        * Keycloak admin user=admin
        * Keycloak admin password=admin
        * Routing suffix of your OpenShift cluster=cloudservices.skunkhenry.com
        * Eclipse Che version=nightly
        * Keycloak Image=eclipse/che-keycloak
        * Require admin password update=true

--> Creating resources ...
    deploymentconfig "keycloak" created
    service "keycloak" created
    route "keycloak" created
    persistentvolumeclaim "keycloak-data" created
    persistentvolumeclaim "keycloak-log" created
--> Success
    Access your application via route 'keycloak-che.cloudservices.skunkhenry.com' 
    Run 'oc status' to view your app.
$ oc apply -f pvc/che-server-pvc.yaml
persistentvolumeclaim "che-data-volume" created
$ oc new-app -f che-server-template.yaml -p ROUTING_SUFFIX=${ROUTING_SUFFIX} -p CHE_MULTIUSER=true
--> Deploying template "che/che" for "che-server-template.yaml" to project che

     che
     ---------
     Che

     * With parameters:
        * Routing suffix of your OpenShift cluster=cloudservices.skunkhenry.com
        * Eclipse Che version=nightly
        * Eclipse Che server image=docker.io/eclipse/che-server
        * Che Multi-user flavor=true
        * OpenShift Username=
        * OpenShift Password=
        * OpenShift token=
        * HTTP protocol=http
        * Websocket protocol=ws
        * HTTPS support=false
        * OpenShift namespace to create workspace objects=${NAMESPACE}
        * Default PVC claim=1Gi
        * PVC strategy=unique
        * Admin password update=true
        * Identity provider URL=${PROTOCOL}://keycloak-${NAMESPACE}.${ROUTING_SUFFIX}/auth
        * Alias of the Openshift identity provider in Keycloak=NULL
        * Update Strategy=Recreate
        * Che server image pull policy=Always
        * OpenShift master URL=
        * Pre-create subpaths in PV=false
        * GitHub Client ID=
        * GitHub Client Secret=

--> Creating resources ...
    serviceaccount "che" created
    rolebinding "che" created
    service "che-host" created
    route "che" created
    deploymentconfig "che" created
--> Success
    Access your application via route 'che-che.cloudservices.skunkhenry.com' 
    Run 'oc status' to view your app.
$ oc set volume dc/che --add -m /data --name=che-data-volume --claim-name=che-data-volume
deploymentconfig "che" updated
```

* creates a new namespace https://cloudservices.skunkhenry.com:8443/console/project/che/overview
* che dashboard http://che-che.cloudservices.skunkhenry.com/
* keycloak dashboard http://keycloak-che.cloudservices.skunkhenry.com/
  * admin:admin