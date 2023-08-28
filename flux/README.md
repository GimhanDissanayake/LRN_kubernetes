# Install fluxctl
Ref: https://fluxcd.io/flux/installation/#install-the-flux-cli
curl -s https://fluxcd.io/install.sh | sudo bash

# Installing Flux

kubectl create ns flux

## install flux and hook it up to the git repo
GHUSER=


fluxctl install \
--git-user=${GHUSER} \
--git-email=${GHUSER}@users.noreply.github.com \
--git-url=git@github.com:${GHUSER}/docker-development-youtube-series \
--git-path=kubernetes/configmaps,kubernetes/secrets,kubernetes/deployments \
--git-branch=flux-test \
--namespace=flux | kubectl apply -f -

kubectl -n flux rollout status deployment/flux

$env:FLUX_FORWARD_NAMESPACE = "flux"
fluxctl list-workloads
fluxctl identity