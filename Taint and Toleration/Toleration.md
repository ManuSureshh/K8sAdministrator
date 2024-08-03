**Preventing Scheduling**
```
tolerations:
- key: "dedicated"
  operator: "Equal"
  value: "frontend"
  effect: "NoSchedule"
```

**Prefer No Scheduling**
```
tolerations:
- key: "environment"
  operator: "Equal"
  value: "production"
  effect: "PreferNoSchedule"
```

**Eviction of Existing Pods**
```
tolerations:
- key: "role"
  operator: "Equal"
  value: "database"
  effect: "NoExecute"
```

**Special Hardware Requirements**
```
tolerations:
- key: "gpu"
  operator: "Equal"
  value: "true"
  effect: "NoSchedule"
```

**Maintenance Mode**
```
tolerations:
- key: "maintenance"
  operator: "Equal"
  value: "scheduled"
  effect: "NoSchedule"
```

**Node Under High Load**
```
tolerations:
- key: "load"
  operator: "Equal"
  value: "high"
  effect: "NoSchedule"
```

**Specialized Workloads**
```
tolerations:
- key: "specialized"
  operator: "Equal"
  value: "compute"
  effect: "NoSchedule"
```
