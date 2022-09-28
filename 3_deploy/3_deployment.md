# deployment

# 1. create deployment
```
> k apply -f deployment.yaml
> k get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   5/5     5            5           11s
> k rollout status deployment/nginx-deployment
deployment "nginx-deployment" successfully rolled out

```

# 2. inspect deployment
```
> k rollout status deployment/nginx-deployment
deployment "nginx-deployment" successfully rolled out
> k get rs #replicaset
NAME                         DESIRED   CURRENT   READY   AGE
nginx-deployment-dd57ffc87   5         5         5       2m45s
> k get pods
NAME                               READY   STATUS    RESTARTS   AGE
nginx-deployment-dd57ffc87-2lmqv   1/1     Running   0          3m24s
nginx-deployment-dd57ffc87-9tx9n   1/1     Running   0          3m24s
nginx-deployment-dd57ffc87-cft8z   1/1     Running   0          3m24s
nginx-deployment-dd57ffc87-g9xpk   1/1     Running   0          3m24s
nginx-deployment-dd57ffc87-vqtqs   1/1     Running   0          3m24s
```

# 3. update a running deployment
update image:
```
> k set image deployment.v1.apps/nginx-deployment cs-nginx=nginx:1.16.1
deployment.apps/nginx-deployment image updated
> k set image deployment/nginx-deployment cs-nginx=nginx:1.16.2
deployment.apps/nginx-deployment image updated
> k edit deployment/nginx-deployment
> k rollout history deployment/nginx-deployment
> k scale deployment/nginx-deployment --replicas=10

```





