# apis
kubectl api-resources

# pod
```bash
kubectl run nginx --image nginx
kubectl get pods
kubectl get pods --as dev-user

# replicaset
```bash
kubectl create -f replicaset-definition.yml
kubectl get replicaset
kubectl delete replicaset myapp-replicaset
kubectl replace -f replicaset-definition.yml
kubectl scale --replicas=6 -f replicaset-definition.yml
kubectl scale --replicas=6 replicaset myapp-replicaset

# deployment
```bash
kubectl create -f deployment-definition.yml
kubectl apply -f deployment-definition.yml
kubectl get deployments
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment/myapp-deployment
kubectl rollout undo deployment/myapp-deployment
kubectl expose deployment nginx --port 80
kubectl scale deployment nginx --replicas=5
kubectl replace –f nginx.yaml
kubectl edit deployment nginx

# service
```bash
db-service.dev.svc.cluster.local
ServiceName.Namespace.Service.domain

# kube config
```bash
kubectl config set-context $(kubectl config current-context) --namespace=dev

# Container runtimes
```bash
ctr
nerdctl
crictl
crictl ps -a
crictl logs container-id
watch crictl ps

Container Runtime Interface (CRI)
Open Container Initiative (OCI) - imagespec, runtimespec

# Node
```bash
kubectl get nodes
k describe node controlplane
k drain node01 --ignore-daemonsets
k uncordon node01

# namespace
```bash
kubectl create namespace dev

# etcd
## backup
ETCDCTL_API=3 etcdctl snapshot save /opt/snapshot-pre-boot.db \
--cert="/etc/kubernetes/pki/etcd/server.crt" \
--key="/etc/kubernetes/pki/etcd/server.key" \
--cacert="/etc/kubernetes/pki/etcd/ca.crt" \
--endpoints="127.0.0.1:2379"

## check status
etcdutl snapshot status /opt/snapshot-pre-boot.db
etcdutl --write-out=table snapshot status snapshot.db 

## restore
export ETCDCTL_API=3 etcdctl --data-dir <data-dir-location> snapshot restore snapshot.db

etcdutl --data-dir <data-dir-location> snapshot restore snapshot.db

  ...
  volumes:
  - hostPath:
      path: /var/lib/etcd-from-backup # New restored backup directory
      type: DirectoryOrCreate
    name: etcd-data

## certificates
openssl x509 -in file-path.crt -text -noout

### CertificateSigningRequest
cat akshay.csr | base64 -w 0
```
```
k apply -f - <<EOF
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: akshay
spec:
  groups:
  - system:authenticated
  request: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1ZqQ0NBVDRDQVFBd0VURVBNQTBHQTFVRUF3d0dZV3R6YUdGNU1JSUJJakFOQmdrcWhraUc5dzBCQVFFRgpBQU9DQVE4QU1JSUJDZ0tDQVFFQTNUVFFTREpuQUYvb21KWFU0cFh5T0FOdUV1ektzdE1pWGQrUDZhbWUvemJUCnpRc3ZhcEprWXNET3dNb0FjbHlCd0tFTTVEYVJsMjQ1STRLM0xGanFYL3RPQUlvL0lrY2JQZzNVOWxWeG02VjgKZys5MkkxditqWDljdktVRTJqazJqeGRudmR6NEZZR3QyR29VcjJTL2FCbCt3aGJQMDk3L0pGbUZwTGM4TERadgp1WnNqNTcwL0hTSWVCMnk2dVZJQ0d4NTRKcUxSemM0NFZWMDhxMlEzUHNmY3YvUUV4VloyMEcwV2pLQ1g2SS9LCkNpanMvdUtlc0xYMkhIcUpZUkVTdDZWYTVVTXNUSGFzOUVsbEFTYTVtWTRIM0NGU3RCM2xWTDlmM3dqSkUwNGcKYkl6MXVFanYzWStYZXRvRFAvcUVTKzR5UTc1N0FTRWEvVTdHM2xkOVFRSURBUUFCb0FBd0RRWUpLb1pJaHZjTgpBUUVMQlFBRGdnRUJBSjhsWGNRMW1WbzdqT3EzMldlUU5qQ2JQZU5KaVNqZFNBbWdDN2ZqdkZodjVjU2x2d0dsCm56Nm9uaVRGZU5GamJsQlhZNkc5Wk1menE0TFlVS0pVckMzd21UcTdHUWQ0bnk4QXdUV1ZwRFdZNjhIRVBQTkMKdEFTWk1BdnhxbWhDZ0FaMFIwRXRTbUsvYWxoU1BwVC9NdmFFQVF2bENwbDFzMzc1Y3B5WnRnUGlXRHd1SmZiQgo5Wm5jRGp6N1cyRlpXNUFmVmZRbmQrUXEyNmVqWHdHcXdONnJYY1R2bGdJbWRoSHg1amd2citYK1pJTzlYN2dQCjU3VmJvaTV6TWRFdEtkck1KRnFlTWlvTGVuWnJDKzg3SXl3RWZEQkVwRUVzL0x3OTFaRE9BNjRIVkxUbXZYTFkKSzU1eU82VmNZS1YrTnhVSmIwVmtqa2JhYm8vNHlOYjFXWDA9Ci0tLS0tRU5EIENFUlRJRklDQVRFIFJFUVVFU1QtLS0tLQo=
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
EOF
```
kubectl certificate approve akshay

## kubeconfig
k config --kubeconfig=/root/my-kube-config get-contexts
kubectl config --kubeconfig=/root/my-kube-config use-context <context>
kubectl config --kubeconfig=/root/my-kube-config current-context
### Set the my-kube-config file as the default kubeconfig file
vi ~/.bashrc
export KUBECONFIG=/root/my-kube-config
source ~/.bashrc

# rbac