## What is Replication Controller?
- A `Replication Controller` in Kubernetes ensures that a specified number of pod replicas are running at any given time. 
- If a pod fails or is deleted, the Replication Controller creates a new one to replace it, maintaining the desired number of replicas.

## What are the drawbacks of Replication Controller (RC)?
- `Replication Controller will not reuse the Old Pods`.

  i.e.
    - If we deploy RC with 4 replicas, it will always make sure 4 pods are running.
    - If 1 pod goes down, it will replace it with a new pod.
    - And if that pod comes live, it will not reuse the pod.
