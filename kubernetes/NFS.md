
<div align="center">

# **NFS**

</div>


installing a NFS server to the cluster nodes (workers).

## Prerequisites:

setting a linux server and adding it to the cluster network.

## Deploy and configure NFS server

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

## Prepare Kubernetes worker nodes

on each of the workers node

      apt install -y nfs-common

## test connectivity

mount a drive on the worker node to check NFS (<NFS_IP> - NFS server IP, /dta/shered - folder shered on the NFS server, /home/ec/test - folder in worker node).

      sudo mount <NFS_IP>:/data/shered /home/ec/test

      add a file in the /home/ec/test and check if existed on the NFS server (/dta/shered).

unmount the drive (after checking):

      sudo umount /home/ec/test

# Using NFS in Kubernetes

## Method 1 — Connecting to NFS directly with Pod manifest

connect to the NFS storage directly using the Pod manifest.

      apiVersion: v1
      kind: Pod
      metadata:
        name: test
        labels:
          app.kubernetes.io/name: alpine
          app.kubernetes.io/part-of: kubernetes-complete-reference
          app.kubernetes.io/created-by: ssbostan
      spec:
        containers:
          - name: alpine
            image: alpine:latest
            command:
              - touch
              - /data/test
            volumeMounts:
              - name: nfs-volume
                mountPath: /data
        volumes:
          - name: nfs-volume
            nfs:
              server: node004.b9tcluster.local
              path: /data
              readOnly: no

## Method 2 — Connecting using the PersistentVolume (PV)

create the PersistentVolume object for the NFS volume

      apiVersion: v1
      kind: PersistentVolume
      metadata:
        name: nfs-volume
        labels:
          storage.k8s.io/name: nfs
          storage.k8s.io/part-of: kubernetes-complete-reference
          storage.k8s.io/created-by: ssbostan
      spec:
        accessModes:
          - ReadWriteOnce
          - ReadOnlyMany
          - ReadWriteMany
        capacity:
          storage: 10Gi
        storageClassName: ""
        persistentVolumeReclaimPolicy: Recycle
        volumeMode: Filesystem
        nfs:
          server: node004.b9tcluster.local
          path: /data
          readOnly: no



      
