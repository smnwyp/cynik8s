# 0. start k8s cluster https://kind.sigs.k8s.io/
`> kind create cluster`

# 1. create correct namespace
```
> kubectl get namespaces
NAME                 STATUS   AGE
default              Active   23m
kube-node-lease      Active   23m
kube-public          Active   23m
kube-system          Active   23m
local-path-storage   Active   23m
> kubectl create namespace cynic8s-ns
namespace/cynic8s-ns created
```

# 2. apply pod specification
# 2.1 what is pod?

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. 
A Pod's contents are **always co-located and co-scheduled, and run in a shared context**. 

```
> kubectl --namespace cynic8s-ns apply -f pod.yaml
pod/cynic8s-pod created
```

# 3. how to diagnose what happened?
```
> k get pods --namespace cynic8s-ns
NAME          READY   STATUS    RESTARTS   AGE
cynic8s-pod   1/1     Running   0          35s
> k logs -n cynic8s-ns pod/cynic8s-pod
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.244.0.6. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.244.0.6. Set the 'ServerName' directive globally to suppress this message
[Tue Sep 27 20:37:30.780091 2022] [mpm_event:notice] [pid 1:tid 281473824223248] AH00489: Apache/2.4.54 (Unix) configured -- resuming normal operations
[Tue Sep 27 20:37:30.780170 2022] [core:notice] [pid 1:tid 281473824223248] AH00094: Command line: 'httpd -D FOREGROUND'
```

# 4. how to peek inside the pod created?
```
> kubectl exec -n cynic8s-ns pod/cynic8s-pod -- pwd /   
pwd: ignoring non-option arguments
/usr/local/apache2
> kubectl exec -n cynic8s-ns --stdin --tty pod/cynic8s-pod -- /bin/sh
# pwd
/usr/local/apache2
# exit
```

# 5. how to revert?
```
> k -n cynic8s-ns delete pod --all 
> k delete pod -n cynic8s-ns cynic8s-pod --now   
pod "cynic8s-pod" deleted
> k delete namespace cynic8s-ns
```

# 6. cheatsheet
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
