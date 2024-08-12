# ansible-role-device-lifecycle-manager
Ansible role to create a docker swarm service for Device Lifecycle Manager

This role will deploy Device Lifecycle Manager as a service on docker swarms

Requirements
------------

Docker swarm must be installed and initialized.

Role Variables
--------------

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| dlm_version | Image tag for Device Lifecycle Manager |  |  | yes |
| dlm_application_properties | properties required for Device Lifecycle Manager  | dict | {} | yes |
| service_name | Name of the service that will run DLM  | string | daas-service | no |
| dlm_replicas | Number of replicas the service can spin up on docker swarm | number | 1 | no |
