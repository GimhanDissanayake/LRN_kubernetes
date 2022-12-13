# K8s Service Account(sa)

## Usage
Use when we need to manage K8s resources(pods, deployments, nodes) from inside a pod

## Note

1. Each ns has a default sa which installed automatically with the name "default"
2. You need to manually creat the secret for the sa (after V1.24) or use automountServiceAccountToken: true element
3. No permissions by default
4. Need to use role & role binding to assign permissions
5. Can manage K8s resources via kubenetes API

