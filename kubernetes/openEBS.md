

<div align="center">

# **OpenEBS MayaStore**

</div>

 a software-defined storage solution for Kubernetes that provides persistent storage for applications. It allows you to create and manage storage volumes that can be used by your Kubernetes pods. 
 MayaStore is part of OpenEBS and works well with cloud-native applications, providing scalable and highly available storage.

 Key Features of MayaStore:

   * Dynamic Provisioning: Automatically creates storage volumes when needed by Kubernetes pods.
   * Highly Available: Ensures your data is replicated and available even if a pod or node fails.
   * Snapshot Support: Allows you to take backups of your data.
   * Easy to Use: Seamless integration with Kubernetes for managing persistent storage.


<div align="center">

# **install**

</div>

## Prerequisites

  * minimum 3 workers nodes.
  * each node with an empty drive attached (for the storage).

## install Helm

on each worker node:

     curl -o http://raw.githubusercontent.com/helm/helm/main/script/get-helm-3
     ./get-helm-3

verify installatin:

    helm version

## install nvme-tcp

check if already install

    modinfo nvme-tcp

if not install:

   sudo modprobe nvme-tcp

set it perment (after restart):

  echo "nvme-tcp" | sudo tee -a /etc/modules

## prepering HagePage

(swap must be turn off)

 
