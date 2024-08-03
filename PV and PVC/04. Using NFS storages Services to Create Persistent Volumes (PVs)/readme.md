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
  ```/exported/path *(rw,sync,no_root_squash,no_subtree_check)```
  - `/exported/path`: Directory to be shared.
  - `*`: Allow access from all IPs. You can replace * with specific IPs or subnets for security.
  - `rw`: Read and write access.
  - `sync`: Ensure changes are written to disk before responding.
  - `no_root_squash`: Allows root users on clients to have root access on the server.
  - `no_subtree_check`: Avoid subtree checking for performance improvement.

### Export the Directory
```
sudo exportfs -ra
```

### Verify NFS Access
- On a client machine, test the NFS export
  ```
  sudo mount -t nfs <nfs-server-ip>:/exported/path /mnt
  ```
- Ensure you can read and write to /mnt.


