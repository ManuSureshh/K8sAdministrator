# How Kubernetes components work?

<br>

![image](https://github.com/user-attachments/assets/13c3ace9-0b56-4bae-bcfa-af449e788d11)

<br>

## 1. kubectl Sends a Request to the API Server
- When you execute a command using kubectl (e.g., to create a pod or deploy an application), the request is sent to the Kubernetes API Server.
- The API Server is the central management entity and the gateway to the Kubernetes cluster.

## 2. API Server Processes the Request
- The API Server first authenticates and authorizes the request. It validates the request and updates the cluster's desired state (e.g., adding a new pod specification) in its internal state.
- The API Server writes this updated desired state to etcd, which serves as the single source of truth for the entire cluster’s state.

## 3. etcd Stores the Cluster State
- etcd stores all the persistent data of the cluster, including the state of all objects like pods, deployments, services, etc.
- When the API Server writes the new desired state to etcd, it is stored as a consistent snapshot of the cluster’s state.
  
## 4. Scheduler Decides Where to Run the Pod
- If the request is to create a new pod (or other similar resources), the Scheduler becomes involved.
- The Scheduler watches for new pods that do not yet have an assigned node. It queries the API Server to find pods that need scheduling.
- The Scheduler does not talk directly to etcd; instead, it queries the API Server for information (like available resources on nodes) and then makes a decision about where to place the pod.
  
## 5. Scheduler Informs the API Server
- After deciding on the best node for the pod, the Scheduler updates the API Server with the decision.
- The API Server then updates etcd with this scheduling information (e.g., "Pod X should run on Node Y").

## 6. API Server Triggers Controllers
- Once the pod is scheduled to a node, the Controller Manager comes into play. The Controller Manager runs various controllers that watch the current state and attempt to move it towards the desired state.
- For instance, the Node Controller will ensure that the pod is running on the correct node, and the Replication Controller ensures the correct number of pod replicas are running.

## 7. Kubelet Executes the Action
- On the designated worker node, kubelet (the node agent) notices the new pod assignment and pulls the necessary container images, then starts the containers in the pod.
- The kubelet continuously communicates with the API Server to report back the status of the pod (e.g., whether it’s running, failed, etc.).


Summary
---
- `kubectl` → `API Server`: kubectl sends a request to the API Server.
- `API Server` → `etcd`: API Server validates, stores the request, and updates etcd with the desired state.
- `Scheduler` → `API Server`: Scheduler checks with the API Server for pods needing scheduling and decides where to place them.
- `API Server` → `etcd`: API Server updates etcd with the scheduling decision.
- `Controller Manager` → `Kubelet`: Controller Manager ensures the correct number of pods and triggers kubelet on the worker node.
- `Kubelet` → `API Server`: Kubelet starts the pod and reports the status back to the API Server.
