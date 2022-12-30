# Cluster Isolation

## 2 Patterns

1. Physical isolation
    - Sperate cluster for each environment

2. Logical isolation
    - One cluster > Multiple namespaces (Virtual clusters)
    *** Not all objects are namespaced -> nodes, persistant volumes

## Isolation Diamentions (04)

1. Scheduling
    - Resource quotas
    - Node selector
    - Taints and Tolerations
    - Node affinity
    - Pod affinity and anti affinity
    - Pod budgt polices 
    ...
    
2. Networking
    - Network polices
    *** By default K8s has a flat network (any pod can communicate with each other across any namespace)

3. Authentication & Authorization (Access to kube api server)
    - RBAC 
    - Pod identity
    - Encrypting secrets
    ...

4. Containers
    - Scan images and runtime
    - Leverage linux capabilities
    - Pod security policy
    - Pod security context
    ...

## Physical vs Logical Isolation

| First Header              | Physical                  | Logical                           |
| --------------------------| --------------------------| ----------------------------------|
| Pod Density               | Low to medium             | Medium to high                    |
| Cost                      | $$                        | $                                 |
| K8s experience desired    | Low to moderate           | Medium to high                    |
| Security                  | High(Surface is small)    | High                              |
| Blast radius of changes   | Small                     | Big                               |
| Management and operations | Owner Team                | Single or Cross Functional Team   |
| Cost management           | Cost Management Tags      | Complex                           |