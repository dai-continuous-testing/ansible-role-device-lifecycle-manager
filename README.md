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
| dlm_version | Image tag for Device Lifecycle Manager | string | latest | yes |
| dlm_application_properties | properties required for Device Lifecycle Manager  | dict | {} | yes |
| service_name | Name of the service that will run DLM  | string | daas-service | no |
| dlm_replicas | Number of replicas the service can spin up on docker swarm | number | 1 | no |
| dlm_p12_password | Password for p12 certificate being used for supervision  | string | '' | yes |
| supervision_p12_path | Path to p12 certificate being used for supervision  | string | '' | yes |
| dlm_internet_secrets | WiFi details for maintenance.internet.authentication  | dict | defaults/main.yml | yes |
