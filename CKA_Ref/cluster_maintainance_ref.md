# os upgrade

1. drain the node
2. perform upgrade
3. uncordon the node

# cluster upgrade

# control plan

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-cache madison kubeadm

kubeadm version

sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.32.0-1.1' && \
sudo apt-mark hold kubeadm

kubeadm version

sudo kubeadm upgrade plan

sudo kubeadm upgrade apply v1.32.0

kubectl drain <node-to-drain> --ignore-daemonsets

sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.32.0-1.1' kubectl='1.32.0-1.1' && \
sudo apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet

kubectl uncordon <node-to-uncordon>

# worker node
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-cache madison kubeadm

kubeadm version

sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.32.0-1.1' && \
sudo apt-mark hold kubeadm

kubeadm version

sudo kubeadm upgrade node

kubectl drain <node-to-drain> --ignore-daemonsets

sudo apt-mark unhold kubelet && \
sudo apt-get update && sudo apt-get install -y kubelet='1.32.0-1.1' && \
sudo apt-mark hold kubelet

sudo systemctl daemon-reload
sudo systemctl restart kubelet

kubectl uncordon <node-to-uncordon>