## Chapter 5  

### Commands
#### 1. Create, get a service run
``` bash
kubectl create -f kubapp-svc.yaml
kubectl get svc
```

<br>

#### 2. Remotely execute command in running container
```bash
kubectl exec <name_of_the_pod> -- curl -s http://address
```

<br>

#### 4. To configure session affinity
``` bash
kubectl create -f kubapp-svc-affinity.yaml
kubectl exec <name_of_the_pod> -- curl -s http://address
```

<br>

#### 5. Create endpoints, service separately:
``` bash
kubectl create -f kubapp-endpoints.yaml
kubectl create -f kubapp-manual-svc-endpoint.yaml

# Check service's functionality
kubectl exec <name of the pod> -- curl http://ip_of_the_service
```

<br>

#### 6. If you wanna test it with Minikube:
```
minikube service <name of the service>
``` 

<br>

#### 7. For the Ingress testing, 

- activate Ingress addon in minikube first:
``` bash
minikube addons enable ingress
```

- then create the Ingress service (example is [here](Chapter_5/ingress.yaml))
``` bash
kubectl create -f ingress.yaml
```

- check that Ingress service was created successfully
```bash
kubectl get ing
NAME             HOSTS                ADDRESS          PORTS     AGE
kubapp-ingress   kubapp.example.com   192.168.99.100   80        18h
```

-  check Ingress functionality:
``` bash
$ curl 192.168.99.100
```

<br>

#### 8. Readiness Probes
- Edit RC settings:
``` bash
kubectl edit rc kubapp
```

- and add something like:
```yaml
spec:
  containers:
  - name: kubapp
    image: evalle/kubapp
    readinessProbe:
      exec:
        command:
        - ls
        - /var/ready
 ```

- then delete your previos pods and check pods again: 
```yaml
kubectl delete po --all
kubectl get po

 NAME           READY     STATUS    RESTARTS   AGE
kubapp-7hfz8   0/1       Running   0          9m
kubapp-fvhv7   0/1       Running   0          9m
kubapp-lvlxr   0/1       Running   0          9m
```

- To make one of the pods ready run
```
kubectl exec kubapp-7hfz8 -- touch /var/ready
```

- Check pod's status again
```yaml
kubectl get po 
NAME           READY     STATUS    RESTARTS   AGE
kubapp-7hfz8   1/1       Running   0          12m
kubapp-fvhv7   0/1       Running   0          12m
kubapp-lvlxr   0/1       Running   0          12m
```

<br>

#### 9. Running a pod without writing a YAML manifest
```
$ kubectl run dnsutils --image=tutum/dnsutils --generator=run-pod/v1 \
  --command -- sleep infinity
pod "dnsutils" created  
```





