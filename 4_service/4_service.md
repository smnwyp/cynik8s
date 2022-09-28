# 0. motivation
make service accessible via Service and expose the Service to the outside world via Ingress

# 1. what is Service and Ingress
## 1.1 Service
Service is a logical set of Pods and a policy by which to access them inside and outside ofdd a k8s cluster. K8s defines Service as an abstract way to load balance across pods and expose an application deployed on a set of Pods. Pods targeted by a Service is usually determined by a selector.

Service is discoverable with the K8S cluster via the same DNS name

Deployment keeps a set of pods running, Service enables network access to a set of pods.
That said, we could use a deployment without a service to keep a set of identical pods running in the K8s cluster.

Deployment can create and destroy Pods dynamically. the IP of the running set of Pods can change all the time at moment's notice. In this case, how are sets of Pods like this discoverable by other deployment of Pods? --> solution: Services.






K8s gives pods their own IP addresses and a signle DNS name for a set of Pods, and can load-balance across them.

```
> kubectl get pods -l cs-label=proxy -o wide  
> kubectl get pods -l cs-label=proxy -o custom-columns=POD_IP:.status.podIPs
POD_IP
[map[ip:10.244.0.36]]
> k get ep c1-nodeport-service
> k exec cs-nginx-pod -- printenv | grep SERVICE
> kubectl port-forward service/cs-nginx-pod 30163
```


## 1.2 Ingress





