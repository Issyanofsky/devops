<div align="center">

# **Prometheus & Grafana**

![Prometheus](../pic/prometeus.gif)

</div>


__Prometheus__ and __Grafana__ are often used together to monitor and visualize the performance of systems.

  * __Prometheus:__ tool that collects and stores metrics (numerical data) from systems, servers, and applications over time. It pulls data (like CPU usage, memory usage, etc.) from different sources and stores it in a time-series database.
  * __Grafana:__ A visualization tool that helps you create dashboards to display and analyze data collected by tools like Prometheus. It connects to Prometheus (and other data sources) and lets you create interactive graphs to track system performance.

<div align="center">

## **Prometheus**


</div>

there are two type of install Prometheus:

  1. __Prometheus__ use exporters (pod dedicated to pull metrics).
  2. __Kube Prometheus__ use Service Monitor. This installation include __Grafana__ installation (__RECOMENDED (NEWER) VERSION__).

__* Note__ you can set a __Service Monitor__ for retreving metrics from a self created App. so that it "pull" metics from a certain port (need to expose metrics in the app).

# 1. Prometheus Install

      https://prometheus.io/docs/practices/instrumentation/

__installing Prometheus and Grafana__

      https://github.com/Issyanofsky/k8s-monitoring

# 2. Kube-Prometheus Install

__* IMPORTANT__

  * Kube-Prometheus as to be installed on a "local" drive (in case of cloud environment).
  * __Monitoring Ingress__ there a need to reinstall Ingress in order that the __Service Monitor__ will function. in the kube-prometheus there is a need that the Ingress. so the installation process should be: ingress is installed, then install kube-prometheus and after installing agin Ingress.

      helm repo add prometheus-community https://prometheus-community.github.io/helm-chart

      helm repo update prometheus-community

      helm search repo prometheus-community

Download the Chart:

    helm pull prometheus-community/kube-prometheus-stack --untar

edit the value.yml file (*Best practice - make a copy) - it will set the prometheus, grafana (with storage) and set ingress in the cluster:

   set the following values:

        alertmanager:
           enabled: false (change to false. alert can be done from Grafana)

        grafana:
           ingress:
              enabled: true (enable Grafana)
              ingressClassName: nginx (we removed the "#")
              hosts:
                - grafana.domain.com (removed the "[]" and add the domain to publish)
              persistence: (remove the "#" to enable voluve for keeping data)
                 enabled: true
                 type: sts
                 storageClassName: "StorageClassName" (set this to the correct Storage Class Name)
                 accessModes:
                   - ReadWriteOnce
                 size: 20Gi
                 finalizers:
                   - kubernetes.io/pvc-protection
           sidecar:
              datasources:
                 exemplarTraceIdDestinations:
                    alertmanager:
                        enabled: false
        prometheus:
           ingress:
              enabled: True
              hosts:  (removed the "[]" and add the domain to publish)
                - prometheus.domain.com
           prometheusSpec:
               storageSpec: (removed the"{}")
                  volumeClaimTemplate: (removed the"#" frome the next lines)
                     spec:
                       storageClassName: sc (adjust to the storage class name on the cluster)
                       acessModes: ["ReadWriteOnce"]
                       resources:
                          reqests:
                            storage: 50 Gi


Apply the helm chart (install Prometheus and Grafana):

        helm upgrade --install kube-prom-stack prometheus-community/kube-prometheus-stack --name-space monitoring --create-namespace -f value.yaml 

verify Installation:

       kubectl get pods -n monitoring -i "release=kube-prom-stack"

       helm ls -n monitoring

       kubectl get all -n monitoring
