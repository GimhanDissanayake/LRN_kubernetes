https://github.com/kodekloudhub/certified-kubernetes-administrator-course

---
# Certification Details
Note!

In the video, I said the exam is 3 hours. With the latest version of the exam, it is now only 2 hours. The contents of this course has been updated with the changes required for the latest version of the exam.

Below are some references:

Certified Kubernetes Administrator: https://www.cncf.io/certification/cka/

Exam Curriculum (Topics): https://github.com/cncf/curriculum

Candidate Handbook: https://www.cncf.io/certification/candidate-handbook

Exam Tips: http://training.linuxfoundation.org/go//Important-Tips-CKA-CKAD

Head over to this link to enroll in the Certification Exam. Remember to keep the code – 20KODE – handy to get a 20% discount while registering for the CKA exam with Linux Foundation.
---

# COMMANDS
```
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod-definition-1.yaml
kubectl run httpd --image=httpd:alpine --port=80 --expose=true # creat pod and service

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

kubectl scale deployment nginx --replicas=4 

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml # This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option

kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml # This will automatically use the pod’s labels as selectors, but you cannot specify the node port
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml # This will not use the pods labels as selectors

kubectl replace --force -f nginx.yaml # delete the pod and recreate

```