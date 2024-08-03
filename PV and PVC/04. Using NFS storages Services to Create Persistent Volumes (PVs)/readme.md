# Using the NFS server as a storage for Kubernetes cluster
## Prepare the NFS Server
### Install NFS Server
```
sudo apt update
```
```
sudo apt install nfs-kernel-server
```

### Start and Enable NFS Services:
```
sudo systemctl start nfs-server
```
```
sudo systemctl enable nfs-server
```

## Configure Exports
### Edit `/etc/exports`:
- This file defines the directories you want to share over NFS.
```
sudo nano /etc/exports
```
### Add Export Entry
- Add an entry for the directory you want to share. For example:
`/exported/path *(rw,sync,no_root_squash,no_subtree_check)`
