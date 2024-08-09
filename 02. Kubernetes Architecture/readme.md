## How Kubernetes components work?

<br>

![image](https://github.com/user-attachments/assets/13c3ace9-0b56-4bae-bcfa-af449e788d11)

<br>

1. kubectl Sends a Request to the API Server
- When you execute a command using kubectl (e.g., to create a pod or deploy an application), the request is sent to the Kubernetes API Server.
- The API Server is the central management entity and the gateway to the Kubernetes cluster.

2. API Server Processes the Request
- The API Server first authenticates and authorizes the request. It validates the request and updates the cluster's desired state (e.g., adding a new pod specification) in its internal state.
- The API Server writes this updated desired state to etcd, which serves as the single source of truth for the entire cluster’s state.

3. etcd Stores the Cluster State
- etcd stores all the persistent data of the cluster, including the state of all objects like pods, deployments, services, etc.
- When the API Server writes the new desired state to etcd, it is stored as a consistent snapshot of the cluster’s state.
  
4. Scheduler Decides Where to Run the Pod

5. Scheduler Informs the API Server

6. API Server Triggers Controllers

7. Kubelet Executes the Action


Summary
---
