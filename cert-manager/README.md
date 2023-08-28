# Cert Manager

1. Issure - link with a CA
2. Certificate object

# Install Helm
```
# Add the Helm repository
helm repo add jetstack https://charts.jetstack.io

# Update your local Helm chart repository cache
helm repo update

# Install CustomResourceDefinitions
--set installCRDs=true when runing helm install
or
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.12.0/cert-manager.crds.yaml

# Install cert-manager
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.12.0 \
  --set installCRDs=true
```

# Instal kubectl apply
Git: https://github.com/cert-manager/cert-manager
Releases > Download yaml

kubectl apply -f cert-manager/cert-manager-v1.12.3.yaml

# Test self signed certificate

```
# Create test ns
kubectl create ns cert-manager-test
kubectl apply -f ./cert-manager/self-signed/issuer.yaml
kubectl apply -f ./cert-manager/self-signed/certificate.yaml

kubectl describe certificate -n cert-manager-test
kubectl get secrets -n cert-manager-test

kubectl delete ns cert-manager-test
```

# Let's Encrypt - ACME

```
# deploy ingress controller 
kubectl create ns ingress-nginx

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/cloud/deploy.yaml

kubectl -n ingress-nginx get pods

kubectl -n ingress-nginx --address 0.0.0.0 port-forward svc/ingress-nginx-controller 80
kubectl -n ingress-nginx --address 0.0.0.0 port-forward svc/ingress-nginx-controller 443

We should be able to access NGINX in the browser and see a 404 Not Found page: http://localhost/ This indicates there are no routes to / and the ingress controller is running

#Grab public ip
curl ifconfig.co or curl ifconfig.co

# Create Let's Encrypt Issuer for our cluster
kubectl apply -f cert-issuer-nginx-ingress.yaml

# check the issuer
kubectl describe clusterissuer letsencrypt-cluster-issuer

# Issue Certificate
kubectl apply -f certificate.yaml

# check the cert has been issued 

kubectl describe certificate example-app

# TLS created as a secret
kubectl get secrets
NAME                  TYPE                                  DATA   AGE
example-app-tls       kubernetes.io/tls                     2      84m
```