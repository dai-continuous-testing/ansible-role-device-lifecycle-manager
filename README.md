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
| otel_enabled | Enable OpenTelemetry Java agent | bool | false | no |
| otel_service_name | OTEL service name | string | device-lifecycle-manager | no |
| otel_deployment_environment | Deployment environment (e.g. dev, staging, prod) | string | dev | no |
| otel_service_namespace | Service namespace | string | daict | no |
| otel_customer | Customer identifier | string | shared-devices | no |
| otel_exporter_endpoint | OTLP exporter endpoint | string | http://grafana-alloy:4317 | no |
| otel_exporter_protocol | OTLP exporter protocol | string | grpc | no |
| otel_logs_exporter | OTEL logs exporter | string | none | no |
| otel_jar_path | Path to the OpenTelemetry Java agent jar in the container | string | /root/otel-javaagent/opentelemetry-javaagent.jar | no |

### Example: Enabling OpenTelemetry via Inventory

Only override what differs per environment — all other OTEL options default in the role:

```yaml
# inventory/group_vars/prod.yml
otel_enabled: true
otel_deployment_environment: "dev"
otel_service_namespace: "daict"
otel_customer: "shared-devices"
```

The role composes all OTEL JVM options internally from these variables and injects the Java agent into `JAVA_OPTS` when `otel_enabled` is `true`.
