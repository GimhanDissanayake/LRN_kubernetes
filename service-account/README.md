# K8s Service Account(sa)

## Usage
Use when we need to manage K8s resources(pods, deployments, nodes) from inside a pod

## Note

1. Each ns has a default sa which installed automatically with the name "default"
2. There is a secret associated with the sa (automatically created with the sa)
3. No permissions by default
4. Need to use role & role binding to assign permissions
5. Can manage K8s resources via kubenetes API

