# 0. Motivation
**ConfigMaps** in k8s is a good choice for static configs, which is stored in k8s configuration db.
This might not be the best tool for usecases with frequet changes.

Many applications rely on configuration which is used during either application initialization or runtime. 
Most of the times there is a requirement to adjust values assigned to configuration parameters. 
ConfigMaps are the Kubernetes way to inject application pods with configuration data. 


ConfigMaps allow you to **decouple** configuration artifacts from image content to keep containerized applications portable. 
This page provides a series of usage examples demonstrating how to create ConfigMaps and configure Pods using data stored in ConfigMaps.



# 1. create the configmap
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#create-a-configmap

```
> k config set-context --current --namespace=cynic8s-ns
> kubectl create configmap <map-name> <data-source>
```

create ConfigMaps from directories, files, or literal values: 
```
> k create -f configmap.yaml
> kubectl create -n cynic8s-ns -f https://kubernetes.io/examples/configmap/configmap-multikeys.yaml
configmap/special-config created
```

verify and inspect:
```
> k describe configmaps -n cynic8s-ns cynic8s-pod-config
> k get configmaps -n cynic8s-ns cynic8s-pod-config -o yaml
> k delete configmap cynic8s-pod-config
```

# 12. create the pod
```
> k apply -f pod.yaml
> kubectl create -f https://kubernetes.io/examples/pods/pod-configmap-volume.yaml
```

# 3. how to connect to the service?
```
> k get pods
NAME     READY   STATUS      RESTARTS   AGE
cs-pod   0/1     Completed   0          79s
> k logs cs-pod
KUBERNETES_SERVICE_HOST=10.96.0.1
PWD=/
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
KUBERNETES_SERVICE_PORT_HTTPS=443
SPECIAL_LEVEL_KEY=very-cs
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
HOME=/root
SHLVL=1
HOSTNAME=cs-pod
LOG_LEVEL=INFO-cs
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_SERVICE_PORT=443
```

