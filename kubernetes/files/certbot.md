<div align="center">

# **CertBot**

</div>

Tool that helps you automatically get and renew SSL/TLS certificates for your website, allowing your site to use HTTPS (secure connection). It interacts with the Let's Encrypt service to get free certificates.

# Kubernetes Install

## 1. Install CerBot on the Cluster

      helm repo add jetstack https://charts.jetstak.il
      helm repo update
      helm update --install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.11.0

## 2. Setting Cluster Issuer

create a YAML file (this example is for Nginx Ingress):

      apiVersion: cert-manager.io/v1
      kind: ClusterIssuer
      metadata:
        name: letsencrypt-prod
      spec:
        acme:
          server: https://acme-v02.api.letsencrypt.org/directory
          email: ecyanofsky@gmail.com
          privateKeySecretRef:
            name: letsencrypt-prod-private-key
          solvers:
            - http01:
                ingress:
                  class: nginx

Deploy the file:

    kubectl apply -f <file_name.yaml>

## 3. Setting Certificate

create a YAML file:

        apiVersion: cert-manager.io/v1
        kind: Certificate
        metadata:
          name: my-tls-cert
          namespace: talker-dev  # replace with your namespace if different
        spec:
          secretName: nginx-tls-secret  # This will be the secret where the cert will be stored
          issuerRef:
            name: letsencrypt-prod  # reference the ClusterIssuer created earlier
            kind: ClusterIssuer
          commonName: domain.com  # replace with your domain name
          dnsNames:
            - domain.com  # replace with your domain names 
            - prometheus.domain.com
            - grafana.domain.com

Deploy the file:

    kubectl apply -f <file_name.yaml>

## 4. Update Ingress 

This will redirect traffic from HTTPS to HTTP.

on the Ingress deployment [Ingress](Ingress.md):

    Add thoses annotations to the Yaml Ingress install:

          metadata.annotations:
              nginx.ingress.kubernetes.io/ssl-redirect: "false"
              nginx.ingress.kubernetes.io/secure-backends: "false"
              nginx.ingress.kubernetes.io/backend-protocol: "HTTP"

            tls:
              - hosts:
                - domain.com
    
            
