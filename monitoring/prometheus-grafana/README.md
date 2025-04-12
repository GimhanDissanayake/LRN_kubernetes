# Create kind cluster
cd monitoring/prometheus-grafana
kind create cluster --name monitoring --image kindest/node:v1.27.3 --config kind.yaml

# Prometheus

- metrics aggregator
- scrape metrics from various metrics endpoints

# Grafana

- use prometheus as a data source and visualize metrics

# Deploy kube-prometheus
Ref: https://prometheus-operator.dev/docs/prologue/quick-start/
1. Check compatible version for k8s version: https://github.com/prometheus-operator/kube-prometheus#kubernetes-compatibility-matrix
2. Download release zip
3. # Create the namespace and CRDs, and then wait for them to be availble before creating the remaining resources
kubectl create -f manifests-release-0.13/setup
4. # Wait until the "servicemonitors" CRD is created. The message "No resources found" means success in this context.
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
5. kubectl create -f manifests-release-0.13/

# Access Prometheus
* Prometheus, Alertmanager, and Grafana dashboards can be accessed quickly using kubectl port-forward
kubectl --namespace monitoring port-forward svc/prometheus-k8s 9090
* Open Prometheus on localhost:9090 in your browser.

# Access Alertmanager
kubectl --namespace monitoring port-forward svc/alertmanager-main 9093
Open Alertmanager on localhost:9093 in your browser.

# Access Grafana 
kubectl --namespace monitoring port-forward svc/grafana 3000

Open Grafana on localhost:3000 in your browser.
You can login with the username admin and password admin.

# Remove kube-prometheus

kubectl delete --ignore-not-found=true -f manifests/ -f manifests/setup

kind delete cluster --name monitoring
