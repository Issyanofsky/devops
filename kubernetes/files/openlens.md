
<div align="center">

# **OpenLens**

</div>

An open-source, community-driven version of Lens, a popular Kubernetes management tool. It provides an easy-to-use graphical interface for managing Kubernetes clusters. With OpenLens, you can view and control your Kubernetes resources, like pods, services, and deployments, all in one place. It's designed to make working with Kubernetes more intuitive by simplifying cluster management and offering features like monitoring, logs, and resource management in a user-friendly way.

## install OpenLens (windows):

    1. Download the installer

          https://github.com/MuhammedKalkan/OpenLens/releases

          Download the latest .exe installer for Windows.

    2. Run the Installer:

Once downloaded, run the installer and follow the on-screen instructions to complete the installation.    

    3. Launch OpenLens:

After installation, you can open OpenLens from your Start menu.

## Configure cluster on Openlens:

    1. Ensure kubectl is configured:

OpenLens uses kubectl configuration to access your Kubernetes clusters. Ensure your kubectl is set up properly and can access your cluster.

to verify if kubectl is working:

          kubectl get nodes

    2. Launch OpenLens:

          Open the OpenLens application on your system.

    3. Add a Cluster in OpenLens:

          On the OpenLens main screen, click on the + button or "Add Cluster" (located in the sidebar or on the dashboard, depending on the version).

    4. Select Your Cluster Configuration:

OpenLens will automatically detect the available kubeconfig files that kubectl uses. You have two options to connect:

__Automatic Connection:__

OpenLens should automatically show the clusters listed in your kubectl config file. Simply select the cluster you want to connect to and click "Add".

__Manual Connection:__

          Click on "Browse" to find your kubeconfig file. By default, this is usually located at ~/.kube/config for most systems.

    

    
