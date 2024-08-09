## What is Replication Controller?
- A `Replication Controller` in Kubernetes ensures that a specified number of pod replicas are running at all times.
- If a pod fails or is deleted, the Replication Controller creates a new one to replace it, maintaining the desired number of replicas.
  
## What are the drawbacks of Replication Controller (RC)?
- `Replication Controller will not reuse the Old Pods`.

  i.e.
    - If we deploy RC with 4 replicas, it will always make sure 4 pods are running.
    - If 1 pod goes down, it will replace it with a new pod.
    - If the failed pod comes back up, it will not be reused or re-added to the count; only the new pods created by the RC are managed.

- `Replication Controller will not handle the updates and rollbacks for Existing Pods`.

  i.e.
    - If you need to update pod configurations (like environment variables, resource limits, or mounted volumes), you would need to redeploy the Replication Controller or manually update the pods.
    - Redeploying the RC will not reuse existing pods; it will create new ones to meet the replica count. Existing pods will not receive the new configuration details unless they are replaced by the new pods.


