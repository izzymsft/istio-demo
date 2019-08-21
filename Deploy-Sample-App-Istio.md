
## Book Info Application

Now, we have set up our Istio profile. We are going to deploy the sample app to evaluate capabilities of Istio

https://istio.io/docs/examples/bookinfo/


## Navigate to your Istio Installation Directory

```shell

cd $ISTIO_HOME

```

## Label the Default Namespace for Istio

The default Istio installation uses automatic sidecar injection. Label the namespace that will host the application with istio-injection=enabled:

```shell
$ kubectl label namespace default istio-injection=enabled

```

## Deploy the BookInfo application using the kubectl command:

```shell
$ kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml

```
## (Optional Step) 

If you disabled automatic sidecar injection during installation and rely on manual sidecar injection, use the istioctl kube-inject command to modify the bookinfo.yaml

```shell

$ kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)

```

## Confirm all services and pods are correctly defined and running:

```shell
$ kubectl get services

$ kubectl get pods
```


## Accessing Grafana
The analytics and monitoring dashboards for Istio are provided by Grafana. Forward the local port 3000 on your client machine to port 3000 on the pod that is running Grafana in your AKS cluster:

```shell
kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000:3000
```

