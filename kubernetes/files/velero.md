<div align="center">

# **Velero**

![Velero](../pic/velero.gif)

</div>

An open-source tool used to back up, restore, and migrate Kubernetes applications and their associated data. It helps you protect your applications by creating backups of your Kubernetes resources (like deployments, services, etc.) and persistent storage (like databases).

In simpler terms, Velero helps you take snapshots (backups) of your Kubernetes apps and their data, so if something goes wrong (like an accidental deletion or a disaster), you can restore everything quickly.

## use cases:

  * __Backup:__ Safeguard your Kubernetes apps and data.
  * __Restore:__ Quickly restore apps and data if something goes wrong.
  * __Migrate:__ Move your apps and data from one Kubernetes cluster to another.

## Install:

First, you need to install the Velero command-line interface (CLI) to interact with Velero.

On Windows:

Download the Velero CLI from :

          https://github.com/vmware-tanzu/velero/releases

Install Velero in Your Kubernetes Cluster

  1. Create a backup storage location: Velero needs a storage location where it will save your backups. You can use cloud storage like AWS S3, Google Cloud Storage, or Azure Blob Storage. Set up your cloud storage and get your access credentials.

  2. Install Velero: 

 Run the following command to install Velero and configure it with your cloud storage (AWS):

           velero install \
            --provider aws \
            --bucket <YOUR_BUCKET_NAME> \
            --secret-file <YOUR_AWS_CREDENTIALS_FILE> \
            --backup-location-config region=<YOUR_AWS_REGION>

Verify the installation:

          kubectl get pods -n velero

## Using Velero to Backup and Restore

  1. __Create a Backup:__

To create a backup of your entire cluster

           velero backup create <BACKUP_NAME> --include-namespaces <namespace-name>

  2. __Restore a Backup:__

To restore a backup

           velero restore create --from-backup <BACKUP_NAME>
