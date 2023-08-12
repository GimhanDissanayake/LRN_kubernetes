# Deployment vs StatefulSets

## Deployment

- Pods share the same  PV
- Pod has a random hash charactered name
- Pods don't have a consistant DNS names
- Non-delicate scaling (no order in scaling up/down. All pods created at the same time on a replicaset)

## Statefulset
- Each pod gets a seperate PV (Dynamic storage provider)
- Pod name => [POD_NAME]-[Ordinal Number]
  Ex: pod-0, pod-01
- PV are not deleted with the pod. If a pod is deleted and created, it get created with the same name and attached to the same PV
- Pods have a consistant DNS names
- Delicate scaling (Highest number deleted first)
*** Doesn't natively support the database replica set behaviors or configurations