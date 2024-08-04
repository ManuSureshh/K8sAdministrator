## NFS as a DynamicProvisioner
- We can use NFS as both static and Dynamic Provisioner
- In NFS as a Dynamic Provisioner, we create StorageClass and PVC. StorageClass will create PV automatically.

`StorageClass.yaml`
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-storage
provisioner: k8s.io/nfs
parameters:
  server: <NFS_SERVER_IP>
  path: <EXPORT_PATH>
reclaimPolicy: Retain # Retail, Recycle, Delete
volumeBindingMode: Immediate # Immediate, WaitForFirstConsumer
```

<br>

`pvc.yaml`
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-nfs-pvc
spec:
  accessModes:
    - ReadWriteMany # should be same as mentioned in StorageClass
  resources:
    requests:
      storage: 10Gi # should be same as mentioned in StorageClass
  storageClassName: nfs-storage 
```
