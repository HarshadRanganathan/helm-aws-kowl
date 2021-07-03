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

1. Update `stages/prod/prod-values.yaml` file with your broker and schema registry url's.
2. Update `alb.ingress.kubernetes.io/certificate-arn` annotation with your ACM arn.
3. Provide the dns hostname to update your route53 records.

```yaml
external-dns.stage.kubernetes.io/hostname: # External DNS hostname
```

## Install/Upgrade Chart

Run below helm command to install/upgrade the helm chart by providing shared and stage specific values.

```bash
helm upgrade -i kowl . -n platform --values=stages/shared-values.yaml --values=stages/prod/prod-values.yaml
```
