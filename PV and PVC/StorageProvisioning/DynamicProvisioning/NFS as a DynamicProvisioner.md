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


Example: -

- Creating a directory at NFS server. The set the permissions and exporting the directory.
![image](https://github.com/user-attachments/assets/981aa139-4a84-4323-97f0-2e9e88ecc4a0)
![image](https://github.com/user-attachments/assets/e6a1e071-eb7b-4a3c-99c8-a9495e38ed46)

- Create a StorageClass and PVC for our Deployment.
`StorageClass.yaml`
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-storage
provisioner: k8s.io/nfs
parameters:
  server: 34.162.245.41
  path: /home/ubuntu/nfs-pro
reclaimPolicy: Retain # Retail, Recycle, Delete
volumeBindingMode: Immediate # Immediate, WaitForFirstConsumer
```

<br>

![image](https://github.com/user-attachments/assets/13a30a9e-6051-4823-9615-8159e5c581f3)
![image](https://github.com/user-attachments/assets/210b4341-d982-457c-a878-1d7c431b32bb)



