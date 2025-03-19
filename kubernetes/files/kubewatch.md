<div align="center">

# **KubeWatch**

![KubeWatch](../pic/kubewatch.gif)

</div>


A simple tool that watches your Kubernetes resources (like Pods, Deployments, Services, etc.) and sends notifications whenever something changes. For example, if a new Pod is created, a Deployment is updated, or a Service is deleted, Kubewatch can notify you via Slack, Email, or other notification channels.

In simple words, Kubewatch is like a "watchdog" for your Kubernetes cluster. It helps you keep track of changes to your resources by sending you alerts in real time.

__Use Cases:__

  * __Real-time Notifications:__ Get alerts when there are changes to your Kubernetes resources.
  * __Monitoring:__ Helps you monitor what’s happening in your cluster without constantly checking manually.
  * __Integration with Messaging Tools:__ Easily integrates with messaging platforms like Slack, making it easy to receive alerts.

## Install Kubewatch:

__Prerequisites:__

 * Kubernetes Cluster: Argo CD requires a running Kubernetes cluster.
 * Helm.

Add the Kubewatch Helm repository:

        helm repo add kubewatch https://github.com/bitnami-labs/kubewatch/releases/download/v0.1.0
        helm repo update

Install Kubewatch:

        helm install kubewatch kubewatch/kubewatch --namespace kubewatch --create-namespace

## Configure Notification Channels

Kubewatch can send notifications to different services like Slack, Email, or Webhook. You need to configure which service you want to receive the alerts on.

 1. __Create a configuration file__ for Kubewatch to tell it where to send notifications (e.g. for Slack, you would need to set up a Slack webhook URL).
 2. __Configure Kubewatch:__

Create a ConfigMap that contains your notification details (like the Slack webhook URL).

Example for Slack:

              apiVersion: v1
              kind: ConfigMap
              metadata:
                name: kubewatch-config
                namespace: kubewatch
              data:
                SLACK_WEBHOOK_URL: "<Your-Slack-Webhook-URL>"

  3. __Apply the ConfigMap:__

Save the above YAML file (e.g., kubewatch-config.yaml) and apply it:

        kubectl apply -f kubewatch-config.yaml

  4. __Verify Kubewatch is Running__

        kubectl get pods -n kubewatch

  5. __Testing Kubewatch__

To test Kubewatch, you can make a change in your Kubernetes cluster (e.g., create a new pod or deploy a new service). Kubewatch should notify you about the change via your configured notification channel.
