# Important Announcement: AWS EKS will no longer maintain and update Calico charts in this repository #
- The current Calico charts will not be updated
- The current Calico charts will be removed from this repository on March 31, 2023
- Current open requests will be redirected to Calico
- You should submit new requests to Calico directly
    - For Calico, please send issues to [Calico repository](http://github.com/projectcalico/calico)
    - For Tigera Operator, please send issues to [Operator repository](http://github.com/tigera/operator)
- We will update and maintain the [AWS docs](https://docs.aws.amazon.com/eks/latest/userguide/calico.html) for Calico installation after the deprecation


# Calico on AWS

## The instructions and charts provided in this repo have been deprecated and will not be updated. The recommended way to install Calico on EKS is via [Tigera Operator](https://github.com/tigera/operator) instead of this helm-chart.
You can follow https://docs.aws.amazon.com/eks/latest/userguide/calico.html for detailed instructions.

<details>
  <summary>Click to expand the older and now deprecated installation instructions</summary>

## Prerequisites

- Kubernetes 1.11+ running on AWS

## Installing the Chart

First add the EKS repository to Helm:

```shell
helm repo add eks https://aws.github.io/eks-charts
```

Install the Calico CRDs:

```shell
kubectl apply -k github.com/aws/eks-charts/tree/master/stable/aws-calico/crds
```

To install the chart with the release name `aws-calico` and default configuration:

```shell
$ helm install --name aws-calico --namespace kube-system eks/aws-calico
```

To install into an EKS cluster where the CNI is already installed, you can run:

```shell
helm upgrade --install --recreate-pods --force aws-calico --namespace kube-system eks/aws-calico
```

If you receive an error similar to `Error: release aws-calico failed: <resource> "aws-calico" already exists`, simply rerun the above command.

## Configuration

The following table lists the configurable parameters for this chart and their default values.

| Parameter                              | Description                                             | Default                         |
|----------------------------------------|---------------------------------------------------------|---------------------------------|
| `calico.typha.image`                   | Calico Typha Image                                      | `quay.io/calico/typha`          |
| `calico.typha.resources`               | Calico Typha Resources                                  | `requests.memory: 64Mi, requests.cpu: 50m, limits.memory: 96Mi, limits.cpu: 100m` |
| `calico.typha.logseverity`             | Calico Typha Log Severity                               | `Info`                          |
| `calico.typha.nodeSelector`            | Calico Typha Node Selector                              | `{ beta.kubernetes.io/os: linux }` |
| `calico.node.extraEnv`                 | Calico Node extra ENV vars                              | `[]`                            |
| `calico.node.image`                    | Calico Node Image                                       | `quay.io/calico/node`           |
| `calico.node.resources`                | Calico Node Resources                                   | `requests.memory: 32Mi, requests.cpu: 20m, limits.memory: 64Mi, limits.cpu: 100m` |
| `calico.node.logseverity`              | Calico Node Log Severity                                | `Info`                          |
| `calico.node.nodeSelector`             | Calico Node Node Selector                               | `{ beta.kubernetes.io/os: linux }` |
| `calico.typha_autoscaler.resources`    | Calico Typha Autoscaler Resources                       | `requests.memory: 16Mi, requests.cpu: 10m, limits.memory: 32Mi, limits.cpu: 10m` |
| `calico.typha_autoscaler.nodeSelector` | Calico Typha Autoscaler Node Selector                   | `{ beta.kubernetes.io/os: linux }` |
| `calico.tag`                           | Calico version                                          | `v3.8.1`                        |
| `fullnameOverride`                     | Override the fullname of the chart                      | `calico`                        |
| `podSecurityPolicy.create`             | Specifies whether podSecurityPolicy and related rbac objects should be created    | `false`                          |
| `serviceAccount.name`                  | The name of the ServiceAccount to use                   | `nil`                           |
| `serviceAccount.create`                | Specifies whether a ServiceAccount should be created    | `true`                          |
| `autoscaler.image`                     | Cluster Proportional Autoscaler Image                   | `k8s.gcr.io/cluster-proportional-autoscaler-amd64` |
| `autoscaler.tag`                       | Cluster Proportional Autoscaler version                 | `1.1.2`                                            |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install` or provide a YAML file containing the values for the above parameters:

```shell
$ helm install --name aws-calico --namespace kube-system eks/aws-calico --values values.yaml
```
</details>
