# Kind 

kind is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

# GIT

https://github.com/kubernetes-sigs/kind

# Install

# For AMD64 / x86_64
```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

# Usage
```
kind create cluster --name prod1 --image kindest/node:v1.27.3
kind delete cluster --name prod1

```

# Option to access the cluster
```
kind get kubeconfig --name prod1 >> config
echo ";" >> config
kind get kubeconfig --name prod2 >> config

kubectl config view
kubectl config get-contexts
kubectl config current-context
kubectl get context staging
kubectl config use-context <context-name>

* alias k8s-prod='kubectl config use-context production'

kubectl config delete-context <context-name>

* kubectl config Usages: https://loft.sh/blog/kubectl-get-context-its-uses-and-how-to-get-started/



```