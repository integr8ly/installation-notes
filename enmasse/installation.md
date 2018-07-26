## Install Guide
http://enmasse.io/documentation/0.21.0/#installation

## Installation Method
Ansible: http://enmasse.io/documentation/0.21.0/#installing_enmasse_using_ansible

## Cluster Admin Requirements
The Enmasse installation requires cluster admin access during the install process only. Once installed, there are no requirements beyond that for cluster admin rights.

## Post Installation
The ansible playbooks will install the Enmasse authentication services. Once complete, Enmasse then needs to be configured with an Address space. This is ultimately a new namespace on Openshift that will host the product console for end users.

The process of creating a new Address space is documented [here](http://enmasse.io/documentation/0.21.0/#creating_an_address_space)