## To provision infrastructure
az login
az set -s "subscription_id"

cd aks/create-aks-cluster-for-testing

terraform init
terraform plan
terraform apply

## Accessing Sensitive Variables
```
terraform output -json | jq -r .client_certificate.value
terraform output -json | jq -r .kube_config.value > ~/.kube/testclusterconfig
```

## Login with Device Code
```
export KUBECONFIG=~/.kube/testclusterconfig

kubelogin convert-kubeconfig

kubectl get nodes

# clean up cached token
kubelogin remove-tokens
```