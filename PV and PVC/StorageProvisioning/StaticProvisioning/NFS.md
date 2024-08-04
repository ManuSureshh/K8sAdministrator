- Iam using NFS server as a storage for my Kubernetes Cluster.
- In static Provisioning, we manually create PVs and then we instruct the PVCs to use the created PVs.
- Let's create PV
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 10Gi #desired storage capacity
  accessModes:
    - ReadWriteMany # This can also be ReadWriteMany, ReadOnlyMany, ReadWriteOnce
  nfs:
    path: /path/to/nfs/export # add the path which is created in NFS server for the PV to use.
    server: nfs-server.example.com # this can also be the IP address of NFS server
  persistentVolumeReclaimPolicy: Retain # this can also be Retain, Recycle and Delete
```  
