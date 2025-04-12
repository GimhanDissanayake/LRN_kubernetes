# Use a SOCKS5 Proxy to Access Private Kubernetes API

```
# The following command starts a SOCKS5 proxy between your client machine and the remote SOCKS server:
# The SSH tunnel continues running in the foreground after you run this:
ssh -D 1080 -q -N username@kubernetes-remote-server.example

-D 1080: opens a SOCKS proxy on local port :1080.
-q: quiet mode. Causes most warning and diagnostic messages to be suppressed.
-N: Do not execute a remote command. Useful for just forwarding ports.
username@kubernetes-remote-server.example: the remote SSH server behind which the Kubernetes cluster is running (eg: a bastion host).
```

# Client configuration

```
# Option 1
export HTTPS_PROXY=socks5://localhost:1080

# Option 2
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LRMEMMW2 # shortened for readability 
    server: https://<API_SERVER_IP_ADRESS>:6443  # the "Kubernetes API" server, in other words the IP address of kubernetes-remote-server.example
    proxy-url: socks5://localhost:1080   # the "SSH SOCKS5 proxy" in the diagram above
  name: default
contexts:
- context:
    cluster: default
    user: default
  name: default
current-context: default
kind: Config
preferences: {}
users:
- name: default
  user:
    client-certificate-data: LS0tLS1CR== # shortened for readability
    client-key-data: LS0tLS1CRUdJT=      # shortened for readability
```