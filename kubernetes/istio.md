<div align="center">

# **Istio**

</div>

A service mesh that helps manage, secure, and observe the communication between microservices in your application.

      https://makeoptim.com/en/service-mesh/kubeadm-kubernetes-istio-setup/

# Install istioctl

      curl -L https://istio.io/downloadIstio | sh -
      cd istio-1.9.2
      export PATH=$PWD/bin:$PATH

Deploy the Istio operator

     istioctl operator init

Install Istio

    kubectl create ns istio-system

    kubectl apply -f - <<EOF
    apiVersion: install.istio.io/v1alpha1
    kind: IstioOperator
    metadata:
      namespace: istio-system
      name: example-istiocontrolplane
    spec:
      profile: default
    EOF

Verify installation:

    kubectl get pod -n istio-system -w

<div align="center">

# **Kiali**

</div>

A visualization tool for Istio. It gives you a graphical interface to see the interactions between your services, and manage your Istio configuration.

## Installing Kiali

      kubectl apply -f https://raw.githubusercontent.com/kiali/kiali/master/deploy/kubernetes/kiali.yaml

Verify Kiali Deployment:

      kubectl get pods -n istio-system

## Expose Kiali Dashboard:

    kubectl port-forward svc/kiali -n istio-system 20001:20001

    
