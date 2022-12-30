# ResourceQuota
  - Limit resouces consumption per namespace
  - Can limit:
    > Compute resources (CPU, Memory,...)
    > Objects (Pods, Services, etc)
  - When enabled, user must specify requests & limits
  - Requests are what's guaranteed
  - Limits are the burst limit when resources are available

# LimitRange (An Admission controller)
  - Validate or mutate requests/limits of incoming requests
  - Ensure incomming requests does not violate LimitRange object in namespace
  - Applies default resource limits for pods that don't specify any

# PodDisruptionBudget
  - Protects against voluntary distruptions
  - Limit the number of pods of a replicated application that are down simultaneously
  - To respect budget > use Eviction API > kubectl drain
  - Fields: (% or integer)
      spec.minAvailable
      spec.maxAvailable
  *** pod disruptions budgets does not work during > node failure, shutdown

# Node Selector
  - constrain to define pod to schedule on a specific node
  - pods that has no 'nodeSelector' can land on any node 

# Node Affinity (RECOMMENDED)
  - Sucessor of Node Selector
  - Similar to nodeSelector > but can define Soft or Hard
  - 2 Types
    requiredDuringSchedulingIgnoredDuringExecution < (Hard)
    preferredDuringSchedulingIgnoredDuringExecution < (Soft)

# Inter Pod Affinity and Anti Affinity
  - Specify on which nodes pod is eligible to be scheduled based on lables on pods that are already running on the node
  - Pod should run in X or should not run in X
  - Types:
      requiredDuringSchedulingIgnoredDuringExecution < (Hard)
      preferredDuringSchedulingIgnoredDuringExecution < (Soft)