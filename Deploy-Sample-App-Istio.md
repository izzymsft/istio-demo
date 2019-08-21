
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

You should get output similar to this:

iekpo@MININT-5RPA920:~/OCP/istio-1.2.4$ kubectl apply -f <(istioctl kube-inject -f samples/bookinfo/platform/kube/bookinfo.yaml)
service/details unchanged
serviceaccount/bookinfo-details unchanged
deployment.apps/details-v1 configured
service/ratings unchanged
serviceaccount/bookinfo-ratings unchanged
deployment.apps/ratings-v1 configured
service/reviews unchanged
serviceaccount/bookinfo-reviews unchanged
deployment.apps/reviews-v1 configured
deployment.apps/reviews-v2 configured
deployment.apps/reviews-v3 configured
service/productpage unchanged
serviceaccount/bookinfo-productpage unchanged
deployment.apps/productpage-v1 configured

```

## Confirm all services and pods are correctly defined and running:

```shell
$ kubectl get services

$ kubectl get pods
```

## Accessing Supplementary Tools and Add-Ons

The instructions below are intended to be used with the demo application, in a production environment, it will be recommended to access the tools installed within the cluster via a Load Balancer service or other appropriate mechanism that is secure while making the resources still accessible to the users that need it.

Additional details are available [here](https://docs.microsoft.com/en-us/azure/aks/istio-install#accessing-the-add-ons) for accessing the tools via port-forwarding. Below are excerpts for Grafana, Prometheus, Jaeger and Kiali

### Accessing Grafana
The analytics and monitoring dashboards for Istio are provided by Grafana. Forward the local port 3000 on your client machine to port 3000 on the pod that is running Grafana in your AKS cluster:

```shell
kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000:3000
```

You can now reach Grafana at the following URL on your client machine - http://localhost:3000.


### Accessing Prometheus
Metrics for Istio are provided by Prometheus. Forward the local port 9090 on your client machine to port 9090 on the pod that is running Prometheus in your AKS cluster:

```shell
kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=prometheus -o jsonpath='{.items[0].metadata.name}') 9090:9090
```

You can now reach the Prometheus expression browser at the following URL on your client machine - http://localhost:9090.

### Jaeger
Tracing within Istio is provided by Jaeger. Forward the local port 16686 on your client machine to port 16686 on the pod that is running Jaeger in your AKS cluster:

```shell
kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686:16686
```

You can now reach the Jaeger tracing user interface at the following URL on your client machine - http://localhost:16686.

### Kiali
A service mesh observability dashboard is provided by Kiali. Forward the local port 20001 on your client machine to port 20001 on the pod that is running Kiali in your AKS cluster:

```shell
kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=kiali -o jsonpath='{.items[0].metadata.name}') 20001:20001
```
You can now reach the Kiali service mesh observability dashboard at the following URL on your client machine - http://localhost:20001/kiali/console/.

### Getting a List of Services Running

```shell
kubectl get services

NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
details       ClusterIP   10.0.51.8      <none>        9080/TCP   10h
kubernetes    ClusterIP   10.0.0.1       <none>        443/TCP    42h
productpage   ClusterIP   10.0.49.237    <none>        9080/TCP   10h
ratings       ClusterIP   10.0.254.35    <none>        9080/TCP   10h
reviews       ClusterIP   10.0.165.242   <none>        9080/TCP   10h
```
### Getting Inside the Pods to Create Traffic Activity

```shell

# Get a list of all the pods currently active
kubectl get pods

# Get the pod name for the ratings app
kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}'

# Get Inside the Pod
kubectl exec -it $(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}') -c ratings -- /bin/bash

# Make a curl Request to the product-page microservice
curl productpage:9080/productpage | grep -o "<title>.*</title>"

```

