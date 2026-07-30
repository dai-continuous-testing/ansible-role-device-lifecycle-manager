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

### OpenTelemetry (observability)

The DLM image ships with the `opentelemetry-spring-boot-starter` (zero-code auto-instrumentation) and sane defaults, but OTel export is **off by default** (`OTEL_SDK_DISABLED=true`). Set `dlm_otel_enabled: true` to turn it on; traces, logs and metrics are then exported over OTLP/gRPC (4317) to Grafana Alloy, all carrying the same resource attributes so they correlate in Grafana. If the collector is unreachable the exporter fails silently and never affects the service.

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| dlm_otel_enabled | Enable OTLP export (traces + logs + metrics) | bool | false | no |
| dlm_otel_service_name | `service.name` resource attribute | string | daas | no |
| dlm_otel_environment | `deployment.environment` resource attribute | string | prod | no |
| dlm_otel_namespace | `service.namespace` resource attribute | string | daict | no |
| dlm_otel_customer | `customer` resource attribute | string | default | no |
| dlm_otel_alloy_host | Grafana Alloy OTLP/gRPC host | string | localhost | no |
| dlm_otel_alloy_port | Grafana Alloy OTLP/gRPC port | number | 4317 | no |
| dlm_otel_alloy_endpoint | Base OTLP endpoint (derived from host/port) | string | http://{{ dlm_otel_alloy_host }}:{{ dlm_otel_alloy_port }} | no |
