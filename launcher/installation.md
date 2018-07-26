## Guide

* Template based Install https://launcher.fabric8.io/docs/minishift-installation.html#installing-launcher-tool_minishift

## Cluster Admin Requirements

Creates a service account (launcher/configmapcontroller)


## Launcher: Template based Install

Clone the Launcher template:

`git clone git@github.com:fabric8-launcher/launcher-openshift-templates.git`

Login to OpenShift:

`oc login <server>`

Create a project:

`oc new-project launcher`

Add the Launcher template:

`cd launcher-openshift-templates`
`oc create -f openshift/launcher-template.yaml`

Install: 

TODO. Ansible?

## Post-install Configuration

### Launcher Config Map


In the `launcher` config-map, blank these values:

* `launcher.missioncontrol.openshift.api.url`
* `launcher.missioncontrol.openshift.console.url`

Fill these in:

* `launcher.keycloak.client.id` = `launcher-public`
* `launcher.keycloak.realm` = `your-realm`
* `launcher.keycloak.url`	= `http://keycloak.example.com/auth`

In the `launcher-clusters` config map, update with the following:

```
- id: cloudservices
  name: "Cloud Services Cluster"
  apiUrl: https://api.mycluster.example.com:8443 
  consoleUrl: https://mycluster.example.com:8443 
  type: pro
```
