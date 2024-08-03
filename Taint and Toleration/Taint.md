**1. Preventing Scheduling**
- This prevents new pods from being scheduled on the node unless they have a matching toleration.
```
kubectl taint nodes <node-name> dedicated=frontend:NoSchedule
```

**2. Prefer No Scheduling**
- This suggests to the scheduler to avoid placing new pods on this node, but it will still allow scheduling if necessary.
```
kubectl taint nodes <node-name> environment=production:PreferNoSchedule
```

**3. Eviction of Existing Pods**
- This not only prevents new pods from being scheduled on the node but also evicts any existing pods that don't tolerate the taint.
```
kubectl taint nodes <node-name> role=database:NoExecute
```

**4. Special Hardware Requirements**
- This indicates that the node has a GPU and only pods with a matching toleration should be scheduled on it.
```
kubectl taint nodes <node-name> gpu=true:NoSchedule
```

**5. Maintenance Mode**
- This marks the node for maintenance, preventing new pods from being scheduled on it.
```
kubectl taint nodes <node-name> maintenance=scheduled:NoSchedule
```

**6. Node Under High Load**
- This taint suggests that the node is under high load and new pods should not be scheduled on it unless they tolerate the taint.
```
kubectl taint nodes <node-name> load=high:NoSchedule
```

**7. Specialized Workloads**
- This indicates that the node is specialized for certain types of workloads, and only pods with a matching toleration should be scheduled on it.
```
kubectl taint nodes <node-name> specialized=compute:NoSchedule
```
