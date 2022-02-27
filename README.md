
# Prerequisites and used components

## EKS cluster provision

First need to provisioned k8s cluster (EKS on AWS in my case), terraform scripts to spin up EKS cluster attached (terraform folder), also instructuions to how provision EKS using terraform you can find in my repo: https://github.com/warolv/eks-demo

  * VPC created with range: 172.16.0.0/16 

  * 2 public/2 private subnets (Production cluster usually will be spinned cross 3 AZ for HA)

  * worker nodes are t3.medium 'on-demand' EC2 instances (no need for spots in this demo)

  * Ingress Nginx will be deployed on cluster after provisioning

  * Cert Manager will be deployed to cluster after provisioning 


### What is NGINX Ingress?

ingress-nginx is an Ingress controller for Kubernetes using NGINX as a reverse proxy and load balancer.
https://github.com/kubernetes/ingress-nginx

### What is a cert-manager?

cert-manager is a native Kubernetes certificate management controller. It can help with issuing certificates from a variety of sources, such as Let’s Encrypt, HashiCorp Vault, Venafi, a simple signing key pair, or self signed.
It will ensure certificates are valid and up to date, and attempt to renew certificates at a configured time before expiry.
It is loosely based upon the work of kube-lego and has borrowed some wisdom from other similar projects such as kube-cert-manager.

### Using Ingress Nginx as ingress on EKS as Cert Manager to issue self signed certificates

I will use Ingress Nginx as k8s ingress controller (use Classic Load Balancer) and Cert Manager to issue 'self signed' certificates for this solution (using it to issue Let's Encrypt certs in production use cases)

You can read in my post how I am using those components to secure traffic to your application: https://talks.cloudify.co/secure-traffic-to-your-application-with-kubernetes-and-cert-manager-cc2b44d29beb


# Problem

* Deploy 2 services on Kubernetes - which will function via http/s

* Install and configure 2 routes, each service should expose an endpoint
named
  * “/routea” pointing 2 service A
  * “/routeb” pointing to service B


# Solution
  
  In case you not deployed ingress-nginx and cert manager as part of EKS provision with terraform, you can do it manually with helm:


  Let's deploy first service to 'a-ns' namespace

  Let's deploy second service to 'b-ns' namespace



