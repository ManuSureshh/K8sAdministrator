

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
  name: hardware-resources
  namespace: devops-engineer
spec:
  hard:
    requests.cpu: "4"
    requests.memory: "8Gi"
    limits.cpu: "8"
    limits.memory: "16Gi"
```
