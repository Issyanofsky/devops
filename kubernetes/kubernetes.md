    
   <div align="center">

# **kubernetes**

</div>

this is a installation of a cluster contining 1 Control plane (there a need to install a LoadBalancer for more then one Control plane (like HAProxy)).

* Tip: if installing using VM. can install one mechine (till init step) and duplicate them. to avoiud installing each node (only needed to set: hotsname, hosts and IP address).

# Installing

    https://medium.com/@subhampradhan966/kubeadm-setup-for-ubuntu-24-04-lts-f6a5fc67f0df

## 1. Prerequisites:

    * At least two Ubuntu 24.04 LTS servers with 2GB RAM and 2 CPU cores each.
    * Network connectivity between servers (bridge).
    * Root access to each server. set SSH for each server node (Control and Working plane's).

## 2. Update the system and install dependencies:

in each node:

        sudo apt update && sudo apt upgrade -y
        sudo apt install apt-transport-https curl -y
    
Install containerd:

        sudo apt install containerd -y

Configure containerd:

        sudo mkdir -p /etc/containerd
        containerd config default | sudo tee /etc/containerd/config.toml > /dev/null
        sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml
        sudo systemctl restart containerd

Install Kubernetes components (you can set here the version to install by setting the command):

        curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
        echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
        sudo apt update
        sudo apt install -y kubelet kubeadm kubectl
        sudo apt-mark hold kubelet kubeadm kubectl

Disable swap:

        sudo swapoff -a
        sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab - setting it permenetly - can done manualy by adding "#" on the swap line in sudo nano /etc/fstab).

Load necessary kernel modules:

        sudo modprobe overlay
        sudo modprobe br_netfilter

    set it permemnet (after restart):

        sudo nano /etc/modules-load.d/modules.conf

    Add the following lines:

        overlay
        br_netfilter

        
        
        

        
    
