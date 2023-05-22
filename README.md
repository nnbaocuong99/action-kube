###### Examples: from ["Kubernetes in Action"](https://www.manning.com/books/kubernetes-in-action) by Marko Luksa

## Table of Contents

### Chapter 2
- Docker and Kubernetes.
   - [Dockerfile.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter%202/Dockerfile)
   - Demo-app.

### Chapter 3
- Deploying containers in pods.
  - [Custom namespace.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter%203/app.yaml)
  - App / app + label.
  - Liveness / schedule.

### Chapter 4
- Keep running, replicating pods.
  - [Daemon set.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter%204/daemonset.yaml)
  - RC/RS.

### Chapter 5
- Exposing pods as a service.
  - External name/IP.
  - Headless.
  - [Ingress.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_5/ingress.yaml)
  - [Endpoints](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_5/headless.yaml)
  - [Loadbalancer](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_5/loadbalancer.yaml)
  - Svc, svc affinity
  - Nodeport

### Chapter 6
- Share disk storage between containers in a pod.
  - Nfs.
    - Busybox.
    - Pv, pvc.
    - Server RC, services.
    - Web rc, services.
  - [Dockerfile.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_6/Dockerfile)
  - Repo.
  - Pod.
  - [Server Pod.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_6/server-pod.yaml)
  - Aws/Gce/Nfs/Volume.

### Chapter 7
- Passing configurations, sensitive information
  - [Dockerfile.](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_7/Dockerfile)
  - Pod
  - [Fortuneloop.sh](https://github.com/nnbaocuong99/action-kube/blob/main/Chapter_7/fortuneloop.sh)

---

> ***Warning*** |
All commands below are backup commands

###### k8s
```shell
> minikube start
> kubectl cluster-info

> kubectl get nodes
> kubectl describe node <NODE_ID>
```

<br>

###### Ingress config
```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: kubia
spec:
  rules:
    - host:
      http:
        paths:
          - path: usr/src/nodepoert
            backend:
              serviceName: 
              servicePort: 80
          - path: /usr 
            backend:
              serviceName: user-svc
              servicePort: 90
    - host:
      http:
        paths:
          - path: /
            backend:
              serviceName: 
              servicePort: 8080
```

<br>

###### pod, node select, `yaml` backup
```yaml
apiVersion:
kind: 
metadata:
  name: 
spec:
  containers:
    - image:
      name:
      ports:
        - containerPort: 8080
          protocol: TCP ("SCTP", "TCP", "UDP")
```

```shell
> kubectl get pod -o yaml
> kubectl logs -c 
> kubectl logs -previous
> minikube ssh && docker ps
> docker logs ID
> kubectl port-forward kubia-manual 8081:8080

```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name:
  labels:
    creation_method: 
    env: prod
spec:
```

```shell
> kubectl get pods -l env=debug
> kubectl get pod -l creation_method!=manual
> kubectl get pods -l '!env'
> kubectl get pods -l 'env in (debug)
> kubectl get pods -l 'env notin (debug,online)
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: 
spec:
  nodeSelector:
    gpu: "true"
  containers:
```

<br>

###### namespace
```shell
> kubectl get ns
> kubectl get pods -n kube-system
```

```yaml
apiVersion:
kind: Pod
metadata:
  name: 
  namespace: namespace
spec:
```

```shell
> kubectl config set-context $(kubectl current config) --namespace custom-namespace 
```

<br>

###### Services
```yaml
apiVersion: v1
kind: Service
metadata:
  name:
spec:
  sessionAffinity: ClientIP
  ports:
    - name: http
      port: 80
      targetPort: http
    - name: https
      port: 443
      targetPort: https
  selector:
    app:
```

<br>

###### K8s doesnt assign IPs to the Headless service (all backend pods can be directly discovered through DNS.)
```shell
> kubectl get svc                       
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kube            LoadBalancer   10.104.124.106   <pending>     80:32110/TCP   123m
headless        ClusterIP      None             <none>        80/TCP         10m

root@spagbo:/
Server:         10.99.0.10
Address:        10.99.0.10#53

Name:   headless.default.svc.cluster.local
Address: 172.17.0.1
Name:   headless.default.svc.cluster.local
Address: 172.17.0.2
Name:   headless.default.svc.cluster.local
Address: 172.17.0.3
Name:   headless.default.svc.cluster.local
Address: 172.17.0.4

root@spagbo:/
Server:         10.99.0.10
Address:        10.99.0.10#53

Name:  default.svc.cluster.local
Address: 10.104.124.106
```

