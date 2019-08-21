# Istio Demo

This repository contains information on how to set up Istio on an AKS Cluster to do a basic demonstration of the capabilities of Istio.

There are steps on how to 
- [Set up the AKS Cluster](Setting-Up-Kubernetes-Cluster.md)
- [Install Istio and Helm Clients Locally](Local-Helm-Istio-Setup.md)
- [Install Istio on the Kubernetes Cluster](Istio-on-AKS-Cluster.md)
- [Configure the Profile for Istio on the Cluster](Istio-on-AKS-Cluster.md#step-4-configuration-profile)
- [Deploy the Sample Demo App](Deploy-Sample-App-Istio.md)
- [Observe the Capabilities of Istio within a Kubernetes Cluster](Deploy-Sample-App-Istio.md#accessing-supplementary-tools-and-add-ons)

The overall objective is to use the demo app(s) to explore the tasks and capabilities documented [here](https://istio.io/docs/tasks/):


- [Traffic Management](https://istio.io/docs/tasks/traffic-management/) - demonstrates Istio's traffic routing features.
  - Request Routing - This task shows you how to configure dynamic request routing to multiple versions of a microservice.
  - Ingress - Controlling ingress traffic for an Istio service mesh.
  - Egress - Controlling egress traffic for an Istio service mesh.
  - Mirroring - This task demonstrates the traffic mirroring/shadowing capabilities of Istio.
  - Traffic Shifting - Shows you how to migrate traffic from an old to new version of a service.
  - TCP Traffic Shifting - Shows you how to migrate TCP traffic from an old to new version of a TCP service.
  - Circuit Breaking - This task shows you how to configure circuit breaking for connections, requests, and outlier detection.
  - Fault Injection - This task shows you how to inject faults to test the resiliency of your application.
  - Request Timeouts - This task shows you how to setup request timeouts in Envoy using Istio.


- [Security](https://istio.io/docs/tasks/security/) - demonstrates how to secure the mesh.

- [Policies](https://istio.io/docs/tasks/policy-enforcement/) - demonstrates policy enforcement features.

- [Telemetry](https://istio.io/docs/tasks/telemetry/) - demonstrates how to collect telemetry information from the mesh.


## Pre-Requisites for Istio and Helm Dependencies
If you are using Windows 10, you will need to set up [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to install [Ubuntu 16.04 LTS](https://www.microsoft.com/store/apps/9pjn388hp8c9). 

This is needed for setting up the Istio and Helm clients. The instructions for setting up these tools are are geared towards Linux/UNIX systems.

Once your WSL is up and running, you will need to do and update and then an upgrade.

```shell
sudo apt-get update
sudo apt-get uprade
```

When you are up-to-date, the next step is to set up the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) for interacting with Azure Resources. The version of the Azure CLI used in this example is **2.0.71**

After you CLI installation is complete, you will need to install Kubectl (Cube Control).
The version of **kubectl** used in this example is **1.15.3**

```shell
# Install kubectl
az aks install-cli

# Verify the version
kubectl version
```
