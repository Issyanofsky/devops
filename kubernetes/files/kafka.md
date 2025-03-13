<div align="center">

# **Kafka (bitnami)**

![Kafka](../pic/kafka.gif)

</div>

Kafka is like a messenger system that helps applications and services communicate with each other in real-time.

__Kafka operator__ a full version of kafka but chargable.

## Installing Kafka (open source)

        helm pull oci://registry-1.io/bitnamicharts/kafka --untar

Edit the value file (if neefing to fetc Prometheus)

        metrics.serviceMonitor.enabled: true 

apply the kafka:

        helm upgrade --install <my-realease> oci://registry-1.docker.io/bitnamicharts/kafka --namespace kafka --create-namespace -f value.yaml
