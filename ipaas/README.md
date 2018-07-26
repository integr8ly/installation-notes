# Ignite Installation notes

Guide: https://access.redhat.com/documentation/en-us/red_hat_fuse/7.0/html-single/integrating_applications_with_ignite/#how-you-use

* No cluster admin access is needed during the installation;
* It doesn't require keycloak;
* Some fuse integrations need third party software to be already deployed (such as amq) which might need extra user permission config since those will be deployed in other openshift namespace(s).

## Bash script

Create a new openshift project:

```sh
$ oc new-project test-igniter
```

Download the installation script:

```sh
$ wget https://raw.githubusercontent.com/syndesisio/fuse-ignite-install/1.3/install_ocp.sh
```

Run the installation script (all arguments are optional):

```sh
$ bash install_ocp.sh \
    --project ignite \
    --route ignite.6a63.fuse-ignite.openshiftapps.com \
    --console https://console.fuse-ignite.openshift.com/console
```

Note: the script will delete the project (if specified).
