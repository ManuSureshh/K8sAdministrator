## NFS as a DynamicProvisioner
- We can use NFS as both static and Dynamic Provisioner
- In NFS as a Dynamic Provisioner, we create StorageClass and PVC. StorageClass will create PV automatically.

## Installing `nfs-client-provisioner`
- In order to use NFS as a Dynamic Provisioner, we need to install the `nfs-client-provisioner`.
```
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
```
```
sudo apt-get install apt-transport-https --yes
```
```
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
```
```
sudo apt-get update
```
```
sudo apt-get install helm
```
```
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner
```
```
helm install nfs-subdir-external-provisioner \
nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set nfs.server=10.124.0.9 \
--set nfs.path=/data/nfs \
--set storageClass.onDelete=true
```
```
# Check pods and storage classes:
kubectl get pod
kubectl get sc
```

<br>

## Creating manifest files
- And while creating StorageClass, we should mention the 
`StorageClass.yaml`
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-storage
provisioner: nfs-subdir-external-provisioner
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


## Example: -

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
provisioner: nfs-subdir-external-provisioner
parameters:
  server: 34.162.245.41
  path: /home/ubuntu/nfs-pro
reclaimPolicy: Retain # Retail, Recycle, Delete
volumeBindingMode: Immediate # Immediate, WaitForFirstConsumer
```

<br>

![image](https://github.com/user-attachments/assets/13a30a9e-6051-4823-9615-8159e5c581f3)
![image](https://github.com/user-attachments/assets/210b4341-d982-457c-a878-1d7c431b32bb)

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

<br>

![image](https://github.com/user-attachments/assets/10101bf6-955a-4452-ac4b-51f866e1d97a)


