<div align="center">

# **System Preformance & Metrics Tools**

![System Preformance & Metrics Tools](../pic/metric.gif)
</div>

Refers to how well an application, server, or infrastructure is performing. It includes aspects like speed, resource usage (CPU, memory, disk), and uptime. Metrics tools are used to track and monitor these performance aspects in real-time to ensure systems are running efficiently, predict potential problems, and improve decision-making.

## Common Metrics Monitored:

  * __CPU Usage:__ How much CPU is being used by the system or application.
  * __Memory Usage:__ Amount of memory being used and available.
  * __Disk Usage:__ Amount of disk space being used and how quickly it fills up.
  * __Response Times:__ How long it takes for the system to respond to requests.
  * __Error Rates:__ Number of errors or failures in requests.
  * __Uptime:__ How long the system has been up and running.
  * __Network Traffic:__ Data being sent and received by the system.

## System Performance & Metrics Tools:

  * [prometheus](/kubernetes/files/prometheus.md): monitoring system and time-series database primarily used for metrics. It collects and stores metrics data (e.g., CPU usage, memory usage, response times) and is commonly used to monitor application and infrastructure performance.
  * [Grafana](/kubernetes/files/prometheus.md): a popular open-source dashboard tool that visualizes metrics collected from systems like Prometheus, InfluxDB, or other monitoring tools.
  * __Nagios:__ a monitoring tool that tracks the status of various systems, network devices, and applications, ensuring that systems are up and running.
  * __Datadog:__ a cloud-based monitoring and analytics platform for infrastructure and application performance.
  * __New Relic:__ is an application performance monitoring (APM) tool that helps monitor the performance of applications in real-time.
  * __AWS CloudWatch:__ monitoring service for AWS resources and applications. It provides detailed insights into performance metrics, logs, and alerts.
  * __Zabbix:__ open-source enterprise-level monitoring solution for monitoring the health of systems, networks, and applications.
  * __Sysdig:__ monitoring and security tool for containers and microservices. It focuses on the health and performance of containers running in environments like Kubernetes.

