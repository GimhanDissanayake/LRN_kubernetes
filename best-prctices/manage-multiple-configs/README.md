# Save config
```
az aks get-credentials --resource-group <resource_group_name> --name <cluster_name> -f .kube/cluster_name
```

# Load configs
```
export KUBECONFIG=~/.kube/config-cluster1:~/.kube/config-cluster2:~/.kube/config-cluster3
```

# Manage configs
```
kubectl config get-contexts

kubectl config get-clusters

kubectl config current-context

kubectl config use-context NEW_CONTEXT_NAME
```

# Troubleshoot - Error resolved by
```
az aks install-cli
```