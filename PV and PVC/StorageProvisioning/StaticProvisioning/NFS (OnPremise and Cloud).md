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

- Now we need to create PVC in order to use the above PV.
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
spec:
  accessModes:
    - ReadWriteMany # Must match the access modes defined in the PV
  resources:
    requests:
      storage: 10Gi # Must be less than or equal to the storage specified in the PV
```

- If we want to use the created PV for our deployments, then we we use the created PVC in the manifest
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - name: nfs-storage
          mountPath: /usr/share/nginx/html # Path inside the container where the PVC is mounted
      volumes:
      - name: nfs-storage
        persistentVolumeClaim:
          claimName: nfs-pvc # Name of the PVC to use
```
