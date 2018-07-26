# Guide

* Template based install: https://access.redhat.com/documentation/en-us/red_hat_3scale/2.2/html-single/infrastructure/#onpremises-installation

## Requirements

* A `ReadWriteMany` volume available, this is a blocker for OpenShift Dedicated as it does not support RWX PVs. OpenShift Dedicated states it supports 3Scale APIcast only (https://www.openshift.com/products/dedicated/).

## Install

Pull the `amp.yml` template.

```bash
curl https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/master/amp/amp.yml > apb.yml
```

Create the resources in the template, providing the routing suffix of the cluster
as the `WILDCARD_DOMAIN`.

```bash
oc new-app -f amp.yml --param WILDCARD_DOMAIN=192.168.0.73.nip.io
```

An output similar to the following will be printed.

```bash
--> Deploying template "3scale/3scale-api-management" for "amp.yml" to project 3scale

     3scale API Management
     ---------
     3scale API Management main system

     Login on https://3scale-admin.192.168.0.73.nip.io as admin/nbyd72fy

     * With parameters:
        * PostgreSQL Connection Password=bAHtE8uWKLtVqLnu # generated
        * ZYNC_SECRET_KEY_BASE=OIN11V7yujrPDgoJ # generated
        * ZYNC_AUTHENTICATION_TOKEN=QchndxLtJvbEUmdc # generated
        * AMP_RELEASE=2.2.0
        * ADMIN_PASSWORD=nbyd72fy # generated
        * ADMIN_USERNAME=admin
        * APICAST_ACCESS_TOKEN=uj0wk0sf # generated
        * ADMIN_ACCESS_TOKEN=14lvcw18ljjh4ftw # generated
        * WILDCARD_DOMAIN=192.168.0.73.nip.io
        * WILDCARD_POLICY=None
        * TENANT_NAME=3scale
        * MySQL User=mysql
        * MySQL Password=q0d1t17l # generated
        * MySQL Database Name=system
        * MySQL Root password.=ie2eb8cf # generated
        * SYSTEM_BACKEND_USERNAME=3scale_api_user
        * SYSTEM_BACKEND_PASSWORD=2jhoy7h2 # generated
        * REDIS_IMAGE=registry.access.redhat.com/rhscl/redis-32-rhel7:3.2
        * MYSQL_IMAGE=registry.access.redhat.com/rhscl/mysql-57-rhel7:5.7-5
        * SYSTEM_BACKEND_SHARED_SECRET=i6whtu1a # generated
        * SYSTEM_APP_SECRET_KEY_BASE=34b811c2122a21e22018647de7a7d5db2537ac60e64b335ab3ad184d53d0657603a472bb64e25550ee5261dc11a406ca2e863d3007ced4a376742ebac8a37648 # generated
        * APICAST_MANAGEMENT_API=status
        * APICAST_OPENSSL_VERIFY=false
        * APICAST_RESPONSE_CODES=true
        * MASTER_NAME=master
        * MASTER_USER=master
        * MASTER_PASSWORD=0u2cx66n # generated
        * MASTER_ACCESS_TOKEN=ft54njbw # generated
        * APICAST_REGISTRY_URL=http://apicast-staging:8090/policies

--> Creating resources ...
    imagestream "amp-system" created
    imagestream "amp-backend" created
    imagestream "amp-apicast" created
    imagestream "amp-wildcard-router" created
    persistentvolumeclaim "system-storage" created
    persistentvolumeclaim "mysql-storage" created
    persistentvolumeclaim "system-redis-storage" created
    persistentvolumeclaim "backend-redis-storage" created
    deploymentconfig "backend-cron" created
    deploymentconfig "backend-redis" created
    deploymentconfig "backend-listener" created
    service "backend-redis" created
    service "backend-listener" created
    service "system-provider" created
    service "system-master" created
    service "system-developer" created
    deploymentconfig "backend-worker" created
    service "system-mysql" created
    service "system-redis" created
    deploymentconfig "system-redis" created
    service "system-sphinx" created
    deploymentconfig "system-sphinx" created
    service "system-memcache" created
    deploymentconfig "system-memcache" created
    route "system-provider-admin-route" created
    route "system-master-admin-route" created
    route "backend-route" created
    route "system-developer-route" created
    deploymentconfig "apicast-staging" created
    service "apicast-staging" created
    deploymentconfig "apicast-production" created
    service "apicast-production" created
    route "api-apicast-staging-route" created
    route "api-apicast-production-route" created
    deploymentconfig "apicast-wildcard-router" created
    service "apicast-wildcard-router" created
    route "apicast-wildcard-router-route" created
    configmap "system" created
    configmap "mysql-extra-conf" created
    configmap "mysql-main-conf" created
    deploymentconfig "system-app" created
    deploymentconfig "system-resque" created
    deploymentconfig "system-sidekiq" created
    deploymentconfig "system-mysql" created
    configmap "redis-config" created
    configmap "smtp" created
    imagestream "postgresql" created
    imagestream "amp-zync" created
    secret "zync" created
    deploymentconfig "zync" created
    service "zync" created
    service "zync-database" created
    deploymentconfig "zync-database" created
--> Success
    Access your application via route '3scale-admin.192.168.0.73.nip.io'
    Access your application via route 'master-admin.192.168.0.73.nip.io'
    Access your application via route 'backend-3scale.192.168.0.73.nip.io'
    Access your application via route '3scale.192.168.0.73.nip.io'
    Access your application via route 'api-3scale-apicast-staging.192.168.0.73.nip.io'
    Access your application via route 'api-3scale-apicast-production.192.168.0.73.nip.io'
    Access your application via route 'apicast-wildcard.192.168.0.73.nip.io'
    Run 'oc status' to view your app.
```
