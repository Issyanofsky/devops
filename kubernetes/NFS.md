
<div align="center">

# **NFS**

</div>


installing a NFS server to the cluster nodes (workers).

# Prerequisites:

setting a linux server and adding it to the cluster network.

# Deploy and configure NFS server

      https://kubedemy.io/kubernetes-storage-part-1-nfs-complete-tutorial

Run the following commands on the node you considered for the NFS server.

      apt update && apt -y upgrade

      apt install -y nfs-server

      mkdir /data

      cat <<EOF >> /etc/exports
      /data <NFS-server_IP> (rw,no_subtree_check,no_root_squash)
      EOF
      (or add maually by editing /etc/exports and adding: /data <NFS-server_IP> (rw,no_subtree_check,no_root_squash))

If needed change perrmission for the folders:

      sudo chmod 777 <folder_name> -R
      sudo chown nobody:nogroup <folder_name> -R

Restart NFS

      sudo systemctl enable --now nfs-server
      sudo   exportfs -ar

# Prepare Kubernetes worker nodes

on each of the workers node

      apt install -y nfs-common
