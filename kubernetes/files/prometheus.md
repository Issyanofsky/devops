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

