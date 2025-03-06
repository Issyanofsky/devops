    
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

Set required sysctl parameters:

        cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
        net.bridge.bridge-nf-call-iptables  = 1
        net.bridge.bridge-nf-call-ip6tables = 1
        net.ipv4.ip_forward                 = 1
        EOF
      
        sudo sysctl --system

* if you have to duplicate the mechines (nodes) this is the phase!!!

## setting each node - HostName, Hosts and IP Address

    setting for each node (mechine): name, host list and IP adress.

    HOSTNAME (server name)

        sudo nano /etc/hostname

        edit the server name (ex. control01)

    HOSTS

    setting HOSTS list of the nodes (and proxy if exist).

        sudo nano /etc/hosts

        add the nodes (and proxy)

            (ex. 192.168.1.80 control01)

    IP Address

    setting each node with a uniqe IP address in the network.

        sudo /etc/netplan/50_config

    edit (change dhcp to false and add the following lines):
        
        dhcp4: false
        addresses: [192.168.1.80/24]
        gateway4: 192.168.1.1
        nameservers:
            adresses: [192.168.1.1, 8.8.8.8]

## Initialize the cluster (run only on Control plane node):

diploying this phase done on ONE Control plane node only (other Controls will initialize with a command that will follow this phase).

    (this line can vary, depend on the cluster architecture like LoadBalancer address and more).
    
        sudo kubeadm init --pod-network-cidr=10.244.0.0/16 

* Importanat: copy the join command needed from the result for using to join the other nodes (there is a join command for Control plane and Worker nodes).
        
 Set up kubeconfig for the user:   

        mkdir -p $HOME/.kube
        sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
        sudo chown $(id -u):$(id -g) $HOME/.kube/config

        export KUBECONFIG=/path/to/cluster-config

Install Flannel network plugin (run only on master node):

        kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

Verify the installation:

        kubectl get nodes
        kubectl get pods --all-namespaces

## Join Other nodes to the cluster:

using the command line to join that was display after the init phase. in each node (not the one alresy init) you need to join to the cluster.

    looks like:

        kubeadm join 172.31.19.36:6443 --token 922x9d.v0jn4c8he0s286js --discovery-token-ca-cert-hash sha256:8897fd8eb97f2ea0686ccf7507f287ffffd5cf681496fb324940330561c80e4c
        
Verify the installation:

        kubectl get nodes
        kubectl get pods --all-namespaces

