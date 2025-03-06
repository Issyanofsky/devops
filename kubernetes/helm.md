
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


