

```
apiVersion: v1
kind: Namespace
metadata:
  name: devops-engineer
  labels:
    name: production
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: object-counts
  namespace: devops-engineer
spec:
  hard:
    pods: "10"
    services: "5"
    configmaps: "10"
    persistentvolumeclaims: "5"
    replicationcontrollers: "5"
    secrets: "10"
    count/deployments.apps: "2"
    count/replicasets.apps: "2"

```
