## What is Replication Controller?
- A `Replication Controller` in Kubernetes ensures that a specified number of pod replicas are running at any given time. 
- If a pod fails or is deleted, the Replication Controller creates a new one to replace it, maintaining the desired number of replicas.

## What are the drawbacks of Replication Controller (RC)?
- `Replication Controller will not reuse the Old Pods`.

  i.e.
    - If we deploy RC with 4 replicas, it will always make sure 4 pods are running.
    - If 1 pod goes down, it will replace it with a new pod.
    - And if that pod comes live, it will not reuse the pod.

- `Replication Controller will not handle the updates and rollbacks for Existing Pods`.

  i.e.
    - Let's say I want to update the Pod configurations (environment variables, resource limits, or mounted volumes), at that time we have to redeploy the Replication Controller.
    - Before redeploying, the pods will be running already. So if I redeploy the Replication Controller, it will not reuse the exsiting pods. Which means, existing pods will not get the configuration details. 



# Kubernetes Replication Controller

## What is a Replication Controller?

A **Replication Controller** in Kubernetes ensures that a specified number of pod replicas are running at all times. If a pod fails or is deleted, the Replication Controller creates a new one to replace it, maintaining the desired number of replicas.

## What are the drawbacks of a Replication Controller (RC)?

### 1. Replication Controller Will Not Reuse Old Pods

- **If you deploy an RC with 4 replicas**, it ensures that 4 pods are always running.
- **If 1 pod fails**, it creates a new one to replace it.
- **If the failed pod comes back up**, it will not be reused or re-added to the count; only the new pods created by the RC are managed.

### 2. Replication Controller Does Not Handle Updates and Rollbacks

- **If you need to update pod configurations** (like environment variables, resource limits, or mounted volumes), you would need to redeploy the Replication Controller or manually update the pods.
- **Redeploying the RC** will not reuse existing pods; it will create new ones to meet the replica count. Existing pods will not receive the new configuration details unless they are replaced by the new pods.

## Alternative: Kubernetes Deployments

For managing updates and rollbacks more effectively, Kubernetes Deployments are recommended. Deployments provide advanced features for handling updates, rollbacks, and scaling in a more controlled manner.

