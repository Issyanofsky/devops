<div align="center">

# **KubeVirt**

![KubeVirt](../pic/kubevirt.gif)

</div>

An extension for Kubernetes that allows you to run virtual machines (VMs) alongside your containerized applications. It brings the power of virtualization into Kubernetes, making it possible to manage both containers and VMs using the same Kubernetes platform.

Lets you run traditional virtual machines (like those you’d run on VMware or VirtualBox) in a Kubernetes environment. This allows you to manage both containers (small, fast apps) and VMs (larger, often more complex applications) in one place.

## Use cases:

  * __Unified Management:__ Manage VMs and containers in one system (Kubernetes).
  * __Hybrid Applications:__ Run legacy apps (that need VMs) and modern apps (that run in containers) together.
  * __Improved Infrastructure Efficiency:__ Take advantage of Kubernetes’ scheduling, scaling, and management features for VMs.

## Install:

__Prerequisites:__

  * a working Kubernetes cluster (on your local machine or cloud).
  * __kubctl__ installed.

Deploy KubeVirt Operator:

Install the KubeVirt operator, which manages the lifecycle of KubeVirt components.

       kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/v0.56.0/kubevirt-operator.yaml

Install KubeVirt
       
       kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/v0.56.0/kubevirt-cr.yaml

Verify Installation

       kubectl get pods -n kubevirt

## Access the KubeVirt UI

To access the UI, expose it with the following command:

       kubectl port-forward svc/virt-manager -n kubevirt 8001:443

access the KubeVirt dashboard:

       https://localhost:8001
