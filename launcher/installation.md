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

TODO