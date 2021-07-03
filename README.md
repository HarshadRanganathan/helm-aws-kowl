# helm-aws-kowl
Example Helm chart for setting up Kowl (Kafka Web Browser) in your Kubernetes cluster.

Chart Reference - https://github.com/cloudhut/charts

## Pre-requisites

### Namespace

Create a new namespace `platform` where we will install the `aws-load-balancer-controller` service.

```bash
kubectl create namespace platform
```

### Config Updates

In `stages/prod/prod-values.yaml` file available inside `stages/prod` folder, add values for below settings:

|||
|--|--|
|brokers |List of broker urls |
|schemaRegistry.urls |List of schema registry urls |
|alb.ingress.kubernetes.io/certificate-arn |ACM certificate arn|
|external-dns.stage.kubernetes.io/hostname<br/>hosts.host[0] |External DNS hostname |

## Install/Upgrade Chart

Run below helm command to install/upgrade the helm chart by providing shared and stage specific values.

```bash
helm upgrade -i kowl . -n platform --values=stages/shared-values.yaml --values=stages/prod/prod-values.yaml
```
