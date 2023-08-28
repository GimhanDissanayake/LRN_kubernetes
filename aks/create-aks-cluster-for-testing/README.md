## To provision infrastructure
az login
az set -s "subscription_id"

terraform init
terraform plan
terraform apply

## Accessing Sensitive Variables
```
terraform output -json | jq -r .client_certificate.value
terraform output -json | jq -r .kube_config.value
```

## Login with Device Code
```
export KUBECONFIG=/path/to/kubeconfig

kubelogin convert-kubeconfig

kubectl get nodes

# clean up cached token
kubelogin remove-tokens
```