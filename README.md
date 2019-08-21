# Istio Demo

This repository contains information on how to set up Istio on an AKS Cluster to do a basic demonstration of the capabilities of Istio.

There are steps on how to 
- [Set up the AKS Cluster](Setting-Up-Kubernetes-Cluster.md)
- [Install Istio and Helm Clients Locally](Local-Helm-Istio-Setup.md)
- [Install Istio on the Kubernetes Cluster](Istio-on-AKS-Cluster.md)
- [Configure the Profile for Istio on the Cluster](Istio-on-AKS-Cluster.md#step-4-configuration-profile)
- [Deploy the Sample Demo App](Deploy-Sample-App-Istio.md)
- [Observe the Capabilities of Istio within a Kubernetes Cluster](Deploy-Sample-App-Istio.md#accessing-supplementary-tools-and-add-ons)

The overall objective is to use the demo app(s) to explore the tasks and capabilities documented here:

https://istio.io/docs/tasks/

## Traffic Management
Tasks that demonstrate Istio's traffic routing features.

https://istio.io/docs/tasks/traffic-management/

## Security
Demonstrates how to secure the mesh.

https://istio.io/docs/tasks/security/

## Policies
Demonstrates policy enforcement features.

https://istio.io/docs/tasks/policy-enforcement/

## Telemetry
Demonstrates how to collect telemetry information from the mesh.

https://istio.io/docs/tasks/telemetry/

If you are using Windows 10, you will need to set up [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to install Ubuntu. 
This is needed for setting up the Istio client. The instructions are for Linux/UNIX systems


