# Using the NFS server as a storage for Kubernetes cluster
## Prepare the NFS Server
1. Install NFS Server
```
sudo apt update
```
```
sudo apt install nfs-kernel-server
```
2. Start and Enable NFS Services:
```
sudo systemctl start nfs-server
```
```
sudo systemctl enable nfs-server
```

