# Install fluxctl
Ref: https://fluxcd.io/flux/installation/#install-the-flux-cli
curl -s https://fluxcd.io/install.sh | sudo bash
curl -s https://fluxcd.io/install.sh | sudo FLUX_VERSION=2.0.0 bash


# Installing Flux

kubectl create ns flux

## install flux and hook it up to the git repo
GHUSER=GimhanDissanayake
ex:
http url: https://github.com/GimhanDissanayake/LRN_kubernetes.git
ssh url: git@github.com:GimhanDissanayake/LRN_kubernetes.git

flux install \
--git-user=${GHUSER} \
--git-email=gimhanem@gmail.com \
--git-url=git@github.com:${GHUSER}/LRN_kubernetes \
--git-path=sampleapp \
--git-branch=development \
--namespace=flux | kubectl apply -f -

kubectl -n flux rollout status deployment/flux

$env:FLUX_FORWARD_NAMESPACE = "flux"
fluxctl list-workloads
fluxctl identity

# Athentication
```
# run fluxctl identity to get the ssh public key to add as a deploy key
fluxctl identity

GIT > 
```

# flux check for changes & sync changes with kubernetes cluster

Default: 5 min
```
# manual sync
fluxctl sync
```

# Annotations
```
  annotations:
    fluxcd.io/tag.example-app: semver:~1.0
    fluxcd.io/automated: 'true'
```

############################################################
# Flux
############################################################
```
# Export Git credentials:
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>

# check your cluster is compatible and ready for Flux:
flux check --pre

# install Flux into our Kubernetes cluster, this is done with the Flux bootstrap command:
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=test-env-infrastructure \
  --branch=main \
  --path=./clusters/dev-cluster-1 \
  --personal

* The bootstrap github command creates the GitHub repository if it doesn’t exists and commits the Flux manifests to the specified branch. Then it configures the target cluster to synchronize with that repository. If the Flux components are present on the cluster, the bootstrap command will perform an upgrade if needed.
Ref: https://fluxcd.io/flux/cmd/flux_bootstrap_github/ 

# Clone the git repository
git clone https://github.com/$GITHUB_USER/fleet-infra
cd fleet-infra

# Testing with podinfo is a tiny web application made with Go.
1. Create a GitRepository manifest pointing to podinfo repository’s master branch:

flux create source git podinfo \
  --url=https://github.com/GimhanDissanayake/podinfo.git  \
  --branch=master \
  --interval=1m \
  --export > ./clusters/dev-cluster-1/podinfo-app/podinfo-source.yaml

2. Commit and push the podinfo-source.yaml file to the fleet-infra repository:
git add -A && git commit -m "Add podinfo GitRepository"
git push

3. Deploy podinfo application
* Configure Flux to build and apply the kustomize directory located in the podinfo repository.
* Use the flux create command to create a Kustomization that applies the podinfo deployment.
flux create kustomization podinfo \
  --target-namespace=default \
  --source=podinfo \
  --path="./manifest" \
  --prune=true \
  --wait=true \
  --interval=1m \
  --retry-interval=2m \
  --health-check-timeout=3m \
  --export > ./clusters/dev-cluster-1/podinfo-app/podinfo-kustomization.yaml

4. Commit and push the Kustomization manifest to the repository:

git add -A && git commit -m "Add podinfo Kustomization"
git push

5. Watch Flux sync the application 
* Use the flux get command to watch the podinfo app.
flux get kustomizations --watch
kubectl -n default get deployments,services

* Changes made to the podinfo Kubernetes manifests in the master branch are reflected in your cluster.

* When a Kubernetes manifest is removed from the podinfo repository, Flux removes it from your cluster. When you delete a Kustomization from the fleet-infra repository, Flux removes all Kubernetes objects previously applied from that Kustomization.

* When you alter the podinfo deployment using kubectl edit, the changes are reverted to match the state described in Git.




```