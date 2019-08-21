
## Download Istio 
https://istio.io/docs/setup/kubernetes/#downloading-the-release

## Set Up Istio Autocompletion
https://istio.io/docs/ops/setup/istioctl/#istioctl-auto-completion


## Customizable Install with Helm

### Helm Client Installation for Ubuntu 16.04 LTS
Install a Helm client with a version higher than 2.10. Get the latest version using the example steps below:

```shell
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get -o get_helm.sh
chmod 0755 get_helm.sh
./get_helm.sh


iekpo@MININT-5RPA920:~/OCP$ ./get_helm.sh
Helm v2.14.3 is available. Changing from version v2.11.0.
Downloading https://get.helm.sh/helm-v2.14.3-linux-amd64.tar.gz
Preparing to install helm and tiller into /usr/local/bin
[sudo] password for iekpo:
helm installed into /usr/local/bin/helm
tiller installed into /usr/local/bin/tiller
Run 'helm init' to configure helm.

helm init
```

```shell 

iekpo@MININT-5RPA920:~/OCP$ helm init
$HELM_HOME has been configured at /home/iekpo/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation

```


## Add the Helm Charts Release Repos

```shell
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.2.4/charts/
```

Option 2: Install with Helm and Tiller via helm install
https://istio.io/docs/setup/kubernetes/install/helm/#option-2-install-with-helm-and-tiller-via-helm-install
