# argocd-infra-deployment

## manual testing

1. apply the example application `k apply -f examples/addons.yaml`
1. check the application with argocd `argocd app sync addons`



## karpenter testing

<https://www.eksworkshop.com/beginner/085_scaling_karpenter/automatic_node_provisioning/>
<https://karpenter.sh/v0.6.1/getting-started/#provisioner>
<https://karpenter.sh/v0.6.1/provisioner/>

1. you will have to update items under `provider` in the `examples/karpenter/provisioner.yaml` file
1. `k apply -f examples/karpenter/provisioner.yaml`
1. `k apply -f examples/karpenter/inflate.yaml`
1. `k scale deployment inflate --replicas 20 -n karpenter`
1. `kubectl logs -f -n karpenter $(kubectl get pods -n karpenter -l karpenter=controller -o name)`
