# bb-argocd-middleware-deployment

- [bb-argocd-middleware-deployment](#bb-argocd-middleware-deployment)
  - [current add-ons](#current-add-ons)
    - [Fluent bit](#fluent-bit)
  - [manual testing](#manual-testing)
    - [addons](#addons)
    - [karpenter testing](#karpenter-testing)
  - [Dev](#dev)
    - [Linting](#linting)

## current add-ons

1. [aws-cloudwatch-metrics](https://aws.github.io/eks-charts)
1. [aws-for-fluent-bit](https://aws.github.io/eks-charts)
1. [karpenter](https://charts.karpenter.sh)
1. [metrics-server](https://kubernetes-sigs.github.io/metrics-server)

### Fluent bit

If you need anything outside of the base fluent-bit configs, update the `add-ons/aws-for-fluent-bit/values.yaml` under the following sections
    * `extraParsers:`
    * `extraInputs:`
    * `extraFilters:`
    * `extraOutputs:`

## manual testing

### addons

1. apply the example application `k apply -f examples/addons.yaml`
1. check the application with argocd `argocd app sync addons`

### karpenter testing

<https://www.eksworkshop.com/beginner/085_scaling_karpenter/automatic_node_provisioning/>
<https://karpenter.sh/v0.6.1/getting-started/#provisioner>
<https://karpenter.sh/v0.6.1/provisioner/>

1. you will have to update items under `provider` in the `examples/karpenter/provisioner.yaml` file
1. `k apply -f examples/karpenter/provisioner.yaml`
1. `k apply -f examples/karpenter/inflate.yaml`
1. `k scale deployment inflate --replicas 20 -n karpenter`
1. `kubectl logs -f -n karpenter $(kubectl get pods -n karpenter -l karpenter=controller -o name)`

## Dev

### Linting

-run these commands on the root of the repository-

```bash
pip install pre-commit-hooks
pre-commit install
pre-commit run --all-files
```
