# Setting Up Istio on the AKS Cluster

## Navigate to the Folder Istio was Downloaded To

```shell
cd ~/istio-1.2.4
```

## Step 0: Begin the Istio pre-installation verification check by running:

Make sure the cluster is ready for Istio Installation

```shell
istioctl verify-install
```

## Step 1: Make sure you have a service account with the cluster-admin role defined for Tiller. If not already defined, create one using following command:

```shell
kubectl --namespace kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
kubectl apply -f install/kubernetes/helm/helm-service-account.yaml
```

## Step 2: Install Tiller on your cluster with the service account:

```shell
helm init --service-account tiller --upgrade
```

## Step 3: Install the istio-init chart to bootstrap all the Istio’s CRDs:

```shell
helm install install/kubernetes/helm/istio-init --name istio-init --namespace istio-system
```

Should get an output similar to the following:

```shell 

NAME:   istio-init
LAST DEPLOYED: Tue Aug 20 21:48:40 2019
NAMESPACE: istio-system
STATUS: DEPLOYED

RESOURCES:
==> v1/ClusterRole
NAME                     AGE
istio-init-istio-system  1s

==> v1/ClusterRoleBinding
NAME                                        AGE
istio-init-admin-role-binding-istio-system  1s

==> v1/ConfigMap
NAME          DATA  AGE
istio-crd-10  1     1s
istio-crd-11  1     1s
istio-crd-12  1     1s

==> v1/Job
NAME               COMPLETIONS  DURATION  AGE
istio-init-crd-10  0/1          0s        1s
istio-init-crd-11  0/1          0s        0s
istio-init-crd-12  0/1          0s        0s

==> v1/Pod(related)
NAME                     READY  STATUS             RESTARTS  AGE
istio-init-crd-10-hs8c5  0/1    ContainerCreating  0         0s
istio-init-crd-11-kzxtf  0/1    ContainerCreating  0         0s
istio-init-crd-12-vz4ht  0/1    ContainerCreating  0         0s

==> v1/ServiceAccount
NAME                        SECRETS  AGE
istio-init-service-account  1        1s

```


## Step 4: Configuration Profile

All the profiles and features are available here: 

https://istio.io/docs/setup/kubernetes/additional-setup/config-profiles/

Select a configuration profile and then install the istio chart corresponding to your chosen profile. 

The default profile is recommended for production deployments, but we will choose the demo profile for our exercise:

```shell
helm install install/kubernetes/helm/istio --name istio --namespace istio-system --values install/kubernetes/helm/istio/values-istio-demo.yaml
```

You should see an output similar to the following:

```shell 

NAME:   istio
LAST DEPLOYED: Tue Aug 20 23:29:02 2019
NAMESPACE: istio-system
STATUS: DEPLOYED

RESOURCES:
==> v1/ClusterRole
NAME                                     AGE
istio-citadel-istio-system               47s
istio-galley-istio-system                48s
istio-grafana-post-install-istio-system  48s
istio-mixer-istio-system                 48s
istio-pilot-istio-system                 48s
istio-reader                             47s
istio-sidecar-injector-istio-system      47s
kiali                                    48s
kiali-viewer                             48s
prometheus-istio-system                  47s

==> v1/ClusterRoleBinding
NAME                                                    AGE
istio-citadel-istio-system                              47s
istio-galley-admin-role-binding-istio-system            47s
istio-grafana-post-install-role-binding-istio-system    47s
istio-kiali-admin-role-binding-istio-system             47s
istio-mixer-admin-role-binding-istio-system             47s
istio-multi                                             47s
istio-pilot-istio-system                                47s
istio-sidecar-injector-admin-role-binding-istio-system  47s
prometheus-istio-system                                 47s

==> v1/ConfigMap
NAME                                                                DATA  AGE
istio                                                               2     48s
istio-galley-configuration                                          1     48s
istio-grafana                                                       2     48s
istio-grafana-configuration-dashboards-galley-dashboard             1     48s
istio-grafana-configuration-dashboards-istio-mesh-dashboard         1     48s
istio-grafana-configuration-dashboards-istio-performance-dashboard  1     48s
istio-grafana-configuration-dashboards-istio-service-dashboard      1     48s
istio-grafana-configuration-dashboards-istio-workload-dashboard     1     48s
istio-grafana-configuration-dashboards-mixer-dashboard              1     48s
istio-grafana-configuration-dashboards-pilot-dashboard              1     48s
istio-grafana-custom-resources                                      2     48s
istio-security-custom-resources                                     2     48s
istio-sidecar-injector                                              2     48s
kiali                                                               1     48s
prometheus                                                          1     48s

==> v1/Deployment
NAME                    READY  UP-TO-DATE  AVAILABLE  AGE
grafana                 0/1    1           0          46s
istio-citadel           1/1    1           1          46s
istio-egressgateway     0/1    1           0          46s
istio-galley            0/1    1           0          46s
istio-ingressgateway    0/1    1           0          46s
istio-pilot             0/1    1           0          46s
istio-policy            1/1    1           1          46s
istio-sidecar-injector  0/1    1           0          45s
istio-telemetry         1/1    1           1          46s
istio-tracing           1/1    1           1          45s
kiali                   1/1    1           1          46s
prometheus              0/1    1           0          46s

==> v1/Pod(related)
NAME                                     READY  STATUS             RESTARTS  AGE
grafana-6fb9f8c5c7-xjfqf                 0/1    ContainerCreating  0         46s
istio-citadel-66866dfc58-jvw5b           1/1    Running            0         45s
istio-egressgateway-6cdc5584cb-9z2gq     0/1    Running            0         46s
istio-galley-b88497745-8v9bs             0/1    ContainerCreating  0         46s
istio-ingressgateway-86c7bf8ccb-54tsn    0/1    Running            0         46s
istio-pilot-77d65b77cf-xktt5             1/2    Running            0         45s
istio-policy-96bd8d589-7q9b2             2/2    Running            0         46s
istio-sidecar-injector-785d58b878-mj7m9  0/1    Running            0         45s
istio-telemetry-98c87d67d-slfw7          2/2    Running            0         46s
istio-tracing-5d8f57c8ff-59m2s           1/1    Running            0         45s
kiali-7d749f9dcb-gspjx                   1/1    Running            0         46s
prometheus-776fdf7479-vs8jr              0/1    Running            0         45s

==> v1/Role
NAME                      AGE
istio-ingressgateway-sds  47s

==> v1/RoleBinding
NAME                      AGE
istio-ingressgateway-sds  47s

==> v1/Secret
NAME   TYPE    DATA  AGE
kiali  Opaque  2     48s

==> v1/Service
NAME                    TYPE          CLUSTER-IP    EXTERNAL-IP  PORT(S)                                                                                                                                     AGE
grafana                 ClusterIP     10.0.248.122  <none>       3000/TCP                                                                                                                                    47s
istio-citadel           ClusterIP     10.0.175.31   <none>       8060/TCP,15014/TCP                                                                                                                          46s
istio-egressgateway     ClusterIP     10.0.62.143   <none>       80/TCP,443/TCP,15443/TCP                                                                                                                    47s
istio-galley            ClusterIP     10.0.38.18    <none>       443/TCP,15014/TCP,9901/TCP                                                                                                                  47s
istio-ingressgateway    LoadBalancer  10.0.87.176   <pending>    15020:30862/TCP,80:31380/TCP,443:31390/TCP,31400:31400/TCP,15029:30320/TCP,15030:30672/TCP,15031:31504/TCP,15032:30776/TCP,15443:31024/TCP  47s
istio-pilot             ClusterIP     10.0.108.113  <none>       15010/TCP,15011/TCP,8080/TCP,15014/TCP                                                                                                      46s
istio-policy            ClusterIP     10.0.245.92   <none>       9091/TCP,15004/TCP,15014/TCP                                                                                                                46s
istio-sidecar-injector  ClusterIP     10.0.206.154  <none>       443/TCP                                                                                                                                     46s
istio-telemetry         ClusterIP     10.0.202.247  <none>       9091/TCP,15004/TCP,15014/TCP,42422/TCP                                                                                                      46s
jaeger-agent            ClusterIP     None          <none>       5775/UDP,6831/UDP,6832/UDP                                                                                                                  45s
jaeger-collector        ClusterIP     10.0.220.158  <none>       14267/TCP,14268/TCP                                                                                                                         45s
jaeger-query            ClusterIP     10.0.115.94   <none>       16686/TCP                                                                                                                                   45s
kiali                   ClusterIP     10.0.247.223  <none>       20001/TCP                                                                                                                                   47s
prometheus              ClusterIP     10.0.36.110   <none>       9090/TCP                                                                                                                                    46s
tracing                 ClusterIP     10.0.202.8    <none>       80/TCP                                                                                                                                      44s
zipkin                  ClusterIP     10.0.147.62   <none>       9411/TCP                                                                                                                                    44s

==> v1/ServiceAccount
NAME                                    SECRETS  AGE
istio-citadel-service-account           1        48s
istio-egressgateway-service-account     1        48s
istio-galley-service-account            1        48s
istio-grafana-post-install-account      1        48s
istio-ingressgateway-service-account    1        48s
istio-mixer-service-account             1        48s
istio-multi                             1        48s
istio-pilot-service-account             1        48s
istio-security-post-install-account     1        48s
istio-sidecar-injector-service-account  1        48s
kiali-service-account                   1        48s
prometheus                              1        48s

==> v1alpha2/attributemanifest
NAME        AGE
istioproxy  44s
kubernetes  44s

==> v1alpha2/handler
NAME           AGE
kubernetesenv  44s
prometheus     44s
stdio          44s

==> v1alpha2/instance
NAME                  AGE
accesslog             44s
attributes            43s
requestcount          44s
requestduration       44s
requestsize           44s
responsesize          43s
tcpaccesslog          43s
tcpbytereceived       44s
tcpbytesent           44s
tcpconnectionsclosed  44s
tcpconnectionsopened  43s

==> v1alpha2/rule
NAME                     AGE
kubeattrgenrulerule      43s
promhttp                 43s
promtcp                  43s
promtcpconnectionclosed  43s
promtcpconnectionopen    43s
stdio                    43s
stdiotcp                 43s
tcpkubeattrgenrulerule   43s

==> v1alpha3/DestinationRule
NAME             AGE
istio-policy     45s
istio-telemetry  45s

==> v1beta1/ClusterRole
NAME                                      AGE
istio-security-post-install-istio-system  47s

==> v1beta1/ClusterRoleBinding
NAME                                                   AGE
istio-security-post-install-role-binding-istio-system  47s

==> v1beta1/MutatingWebhookConfiguration
NAME                    AGE
istio-sidecar-injector  44s

==> v1beta1/PodDisruptionBudget
NAME                    MIN AVAILABLE  MAX UNAVAILABLE  ALLOWED DISRUPTIONS  AGE
istio-egressgateway     1              N/A              0                    49s
istio-galley            1              N/A              0                    49s
istio-ingressgateway    1              N/A              0                    49s
istio-pilot             1              N/A              0                    48s
istio-policy            1              N/A              0                    48s
istio-sidecar-injector  1              N/A              0                    48s
istio-telemetry         1              N/A              0                    48s


NOTES:
Thank you for installing istio.

Your release is named istio.

To get started running application with Istio, execute the following steps:
1. Label namespace that application object will be deployed to by the following command (take default namespace as an example)

$ kubectl label namespace default istio-injection=enabled
$ kubectl get namespace -L istio-injection

2. Deploy your applications

$ kubectl apply -f <your-application>.yaml

For more information on running Istio, visit:
https://istio.io/

```

## Un-Installing Istio from the Cluster

To un-install, use the following commands: 

```shell
$ helm delete --purge istio
$ helm delete --purge istio-init
```

