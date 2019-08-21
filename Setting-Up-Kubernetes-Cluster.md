## Setting Up Kubernetes Cluster on AKS

# Step 1: Set up SSH Keys
```shell
cd ~/.ssh/
ssh-keygen -b 2048 -t rsa -N '' -f istio-demo -C "istio-demo" 
chmod 0600 ~/.ssh/istio-*
```

# Step 2: Create the service principal that will be used for managing the cluster

```shell
az ad sp create-for-rbac --role="Contributor" --name="Istio-Demo-Service-Principal"

AppId                                 DisplayName    Name                  Password                              Tenant
------------------------------------  -------------  --------------------  ------------------------------------  ------------------------------------
602ef24c-fc2d-4b4e-b7bb-d2575369def1  Istio-Demo-SP  http://Istio-Demo-SP  10463c60-d094-44eb-9652-1000b7e2faf9  10f988bf-86f1-41af-91ab-2d7cd011db47

```


# Step 3: Determine the desired region name which supports AKS. I will pick "East US" from the output
```shell
az provider list --query "[?namespace=='Microsoft.ContainerService'].resourceTypes[] | [?resourceType=='managedClusters'].locations[]" -o tsv
```

# Step 4: Verify the supported Kubernetes versions for the desired region. We will pick "1.14.5" from the output

Replace my location using the desired region value from the above step, and then execute:

```shell
az aks get-versions --location "East US" --query "orchestrators[].orchestratorVersion"
```

# Step 5: Create the resource group and deploy the AKS cluster

Replace myResourceGroup and myAKSCluster with desired names, my location using the value from step 3 above, 1.14.5 if not supported in the region, and then execute:

## Create the resource group
```shell
az group create --name IstioDemo --location "East US"
```

## Create the AKS cluster. TODO update to add monitoring

```shell
az aks create --kubernetes-version 1.14.5 --resource-group IstioDemo --name IstioCluster --enable-addons monitoring --service-principal 992ef24c-fc2d-4b4e-b7bb-f2575369def0 --client-secret 80463c60-d094-44eb-9652-1000b7ea8af9 --node-count 3 --node-vm-size Standard_D4s_v3 --ssh-key-value ~/.ssh/istio-demo.pub --location "East US" --max-pods 64
```

### If you do not have SSH keys you can use the --generate-ssh-keys option shown below to generate the keys.
az aks create --resource-group IstioDemo --name IstioCluster --node-count 3 --kubernetes-version 1.14.5 --generate-ssh-keys

```shell
DnsPrefix                    EnableRbac    Fqdn                                                       KubernetesVersion    Location    MaxAgentPools    Name          NodeResourceGroup                 ProvisioningState    ResourceGroup
---------------------------  ------------  ---------------------------------------------------------  -------------------  ----------  ---------------  ------------  --------------------------------  -------------------  ---------------
IstioClust-IstioDemo-86d61f  True          istioclust-istiodemo-86d61f-66127ecf.hcp.eastus.azmk8s.io  1.14.5               eastus      1                IstioCluster  MC_IstioDemo_IstioCluster_eastus  Succeeded            IstioDemo

```

# Step 6: Get the AKS kubeconfig credentials

Replace myResourceGroup and myAKSCluster with the names from the previous step and execute:

```shell
az aks get-credentials --resource-group IstioDemo --name IstioCluster
```

# Step 7: To make full use of the dashboard, since the AKS cluster uses RBAC, a ClusterRoleBinding must be created before you can correctly access the dashboard.

```shell
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

# Step 8 create a proxy tunnel on local port 8001 to the dashboard running on the AKS cluster. 

This CLI command creates a proxy between your local system and the Kubernetes API and opens your web browser to the Kubernetes dashboard.

```shell
az aks browse --resource-group IstioDemo --name IstioCluster
```
