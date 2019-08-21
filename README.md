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
	- **Request Routing** - configuring dynamic request routing to multiple versions of a microservice.
	- **Ingress** - controlling ingress traffic for an Istio service mesh.
	- **Egress** - controlling egress traffic for an Istio service mesh.
	- **Mirroring** - traffic mirroring/shadowing capabilities of Istio.
	- **Traffic Shifting** - how to migrate traffic from an old to new version of a service.
	- **TCP Traffic Shifting** - how to migrate TCP traffic from an old to new version of a TCP service.
	- **Circuit Breaking** - how to configure circuit breaking for connections, requests, and outlier detection.
	- **Fault Injection** - how to inject faults to test the resiliency of your application.
	- **Request Timeouts** - how to setup request timeouts in Envoy using Istio.


- [Security](https://istio.io/docs/tasks/security/) - demonstrates how to secure the mesh.
	- **Authentication Policy** - authentication policy to setup mutual TLS and basic end-user authentication.
	- **Authorization for HTTP Services** - how to set up role-based access control for HTTP services.
	- **Authorization for TCP Services** - how to set up role-based access control for TCP services.	
	- **Authorization for groups and list claims** - configuring the groups-base authorization and configure the authorization of list-typed claims in Istio.
	- **Authorization permissive mode** - how to use Authorization permissive mode.
	- **Istio Vault CA Integration** - how to integrate a Vault Certificate Authority with Istio for mutual TLS.
	- **Mutual TLS Deep-Dive** - how to verify and test Istio's automatic mutual TLS authentication.
	- **Plugging in External CA Key and Certificate** - how operators can configure Citadel with existing root certificate, signing certificate and key.
	- **Citadel Health Checking** - how to enable Citadel health checking with Kubernetes.
	- **Provisioning Identity through SDS** -  how to enable SDS (secret discovery service) for Istio identity provisioning.
	- **Mutual TLS Migration** - how to incrementally migrate your Istio services to mutual TLS.
	- **Mutual TLS over HTTPS** - how to enable mutual TLS on HTTPS services.

- [Policies](https://istio.io/docs/tasks/policy-enforcement/) - demonstrates policy enforcement features.
	- **Enabling Policy Enforcement** - how to enable Istio policy enforcement.
	- **Enabling Rate Limits** - how to use Istio to dynamically limit the traffic to a service.
	- **Control Headers and Routing** - how to modify request headers and routing using policy adapters.
	- **Denials and White/Black Listing** - how to control access to a service using simple denials or white/black listing.

- [Telemetry](https://istio.io/docs/tasks/telemetry/) - demonstrates how to collect telemetry information from the mesh.
	- **Metrics** - demonstrates the configuration, collection, and processing of Istio mesh metrics.
	- **Logs** - demonstrates the configuration, collection, and processing of Istio mesh logs.
	- **Distributed Tracing** - how to configure Istio-enabled applications to collect trace spans.
	- **Visualizing Your Mesh** - how to visualize your services within an Istio mesh.
	- **Remotely Accessing Telemetry Addons** - how to configure external access to the set of Istio telemetry addons.


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
