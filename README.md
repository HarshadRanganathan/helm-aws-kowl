# helm-aws-kowl
Example Helm chart for setting up Kowl (Kafka Web Browser) in your Kubernetes cluster.

Chart Reference - https://github.com/cloudhut/charts

Table of Contents
=================

   * [helm-aws-kowl](#helm-aws-kowl)
      * [Dependencies](#dependencies)
      * [Pre-requisites](#pre-requisites)
         * [Namespace](#namespace)
         * [Config Updates](#config-updates)
      * [Install/Upgrade Chart](#installupgrade-chart)


## Dependencies

[1] External DNS - https://github.com/HarshadRanganathan/helm-aws-external-dns

[2] AWS Load Balancer Controller - https://github.com/HarshadRanganathan/helm-aws-load-balancer-controller


## Pre-requisites

### Namespace

Create a new namespace `platform` where we will install the `aws-load-balancer-controller` service.

```bash
kubectl create namespace platform
```

### ACM

Create a certificate in ACM for your domain

### Config Updates

In `stages/prod/prod-values.yaml` file available inside `stages/prod` folder, add values for below settings:

|||
|--|--|
|brokers |List of broker urls |
|schemaRegistry.urls |List of schema registry urls |
|alb.ingress.kubernetes.io/certificate-arn |ACM certificate arn|
|external-dns.stage.kubernetes.io/hostname<br/>hosts.host[0] |Domain name for external access which will be updated in Route53 |

## Install/Upgrade Chart

Run below helm command to install/upgrade the helm chart by providing shared and stage specific values.

```bash
helm upgrade -i kowl . -n platform --values=stages/shared-values.yaml --values=stages/prod/prod-values.yaml
```
