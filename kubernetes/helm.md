<div align="center">

# **Helm**

</div>

Tool that makes it easier to manage applications on Kubernetes. Think of it like a package manager (similar to apt or npm) but for Kubernetes.

# Installing Helm

## on Linux

      tar -zxvf helm-v3.x.x-linux-amd64.tar.gz
      sudo mv linux-amd64/helm /usr/local/bin/helm

## windows

      https://github.com/helm/helm/releases
      
      Extract the ZIP and add helm.exe to your PATH (e.g., move it to C:\Program Files\Helm and update your system PATH).

Verify Installation:

      helm version

<div align="center">

# **Common Helm Commands**

</div>

## helm install

      helm install <name you give this deployment> <folder with your chart (or a chart from a repo)>
      helm install my-app ./my-chart

recomended

      helm upgrade --install my-app ./my-chart

## helm list

      helm list

      helm ls

## helm uninstall

Removes an app from your cluster.

      helm uninstall <my-app>

## helm repo add

Adds a chart repository.

      helm repo add bitnami https://charts.bitnami.com/bitnami

## helm repo update

Updates your local list of charts from repositories.

      helm repo update

## helm search repo

Finds charts in repositories you’ve added.

      helm search repo wordpress

## helm pull

Downloads a chart to your machine without installing it.

      helm pull bitnami/wordpress

Download the chart to a folder (if need to edit the chart - values file)- using "--untar" 

      helm pull bitnami/wordpress --untar

## helm create

Creates a new chart template to customize (create a folder under the folder the command was execute).

      helm create my-new-chart

