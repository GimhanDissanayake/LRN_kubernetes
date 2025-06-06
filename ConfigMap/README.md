# CongigMap

- API object used to store non-confidential data in key-value pairs. 
- Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.
- A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

- There are four different ways that you can use a ConfigMap to configure a container inside a Pod:

1. Inside a container command and args
2. Environment variables for a container
3. Add a file in read-only volume, for the application to read
4. Write code to run inside the Pod that uses the Kubernetes API to read a ConfigMap