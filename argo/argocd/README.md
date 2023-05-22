# Install Argo CD

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Access The Argo CD API Server
# Port Forwarding
kubectl port-forward svc/argocd-server -n argocd 8080:155.248.231.129:443