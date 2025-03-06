    
   <div align="center">

# **Minikube**

</div>

[follow the steps on (***](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

## windows install

   using PowerShell:

     New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
     
   Add the minikube.exe binary to your PATH (Make sure to run PowerShell as Administrator).

    $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
    if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
    }


## minikube commands

  * minikube start - Start your cluster.
  * minikube pause - Pause Kubernetes without impacting deployed applications.
  * minikube unpause - Unpause a paused instance.
  * minikube stop - Halt the cluster.
  * minikube config set memory 9001 - Change the default memory limit (requires a restart).
  * minikube addons list - Browse the catalog of easily installed Kubernetes services.
  * minikube start -p aged --kubernetes-version=v1.16.1 - Create a second cluster running an older Kubernetes release.
  * minikube delete --all - Delete all of the minikube clusters.
  * minikube status

  minikube start driver=virtualbox --no-vtx-check
 
