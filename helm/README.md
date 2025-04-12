# Helm

## Features

1. Install with one command
2. Create chart versions
3. Upgrade versions
4. Debug deployments
5. Roll back as needed

* Helm templating engine let you pass in data and render values dynamically

https://hub.helm.sh

## Helm charts

Ex: Install > kube-state-metrics
1. Browse through hub and find kubernetes official package

2. Initialize the repo
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

3. To get latest version details
helm repo update

4. Check
helm repo list

5. Create a namespace and install helm chart
kubectl create ns metrics
helm install kube-state-metrics prometheus-community/kube-state-metrics -n metrics

6. Check the deployment of the chart
helm ls -n metrics

7. Check all objects created in the ns
kubectl get all -n metrics

8. kubectl port-forward svc/kube-state-metrics 8080:8080 -n metrics

# COMMANDS

helm show help

helm show chart prometheus-community/kube-state-metrics
helm show values prometheus-community/kube-state-metrics > values.yaml # Easy to read this way rather than pm cmd line

---
# see installed version
helm ls -n metrics

# Upgrade to a specific version
helm upgrade kube-state-metrics prometheus-community/kube-state-metrics --version 0.4.0 -n metrics

# Create a helm chart

```
mkdir temp && cd temp
helm create example-app

# Test the rendering og  our template
helm template example-app example-app
helm template [chart-name] [path to folder where the chart is located]

```
```
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```

