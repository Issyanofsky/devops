
<div align="center">

# **MetalLB**

</div>

MetalLB provides load-balancing functionality for Kubernetes services of type LoadBalancer in environments that don’t have a native cloud provider load balancer.

## Prerequisites

   * kubernetes cluster.
   * cluster doesn’t already have a network load-balancing solution in place.
   * a range of IPv4 addresses available for MetalLB to assign to services (these should be within your network’s subnet and not overlap with other allocations like DHCP).

## Install

        https://metallb.universe.tf/installation/

1. editing kube-proxy config in current cluster:

        kubectl edit configmap -n kube-system kube-proxy

   set:

       strictARP: true

   restart kube-proxy:

       kubectl delete pod -n kube-system kube-proxy (for each kube-proxy pods name).

2. install MetalLB

       kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.9/config/manifests/metallb-native.yaml
   
3. Create Yaml file for setting the metallb

        apiVersion: metallb.io/v1beta1
        kind: IPAddressPool
        metadata:
          name: first-pool
          namespace: metallb-system
        spec:
          addresses:
          - 192.168.1.170-192.168.1.175
        ---
        apiVersion: metallb.io/v1beta1
        kind: L2Advertisement
        metadata:
          name: example
          namespace: metallb-system
        spec:
          ipAddressPools:
          - first-pool

        kubectl apply -f <yaml>

   check:

       kubectl get svc
      
