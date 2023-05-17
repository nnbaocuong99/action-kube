## Chapter 2

#### 1. Use [minikube](https://github.com/kubernetes/minikube)
#### 2. Create image
```bash
docker build -t k8sapp
```

#### 3. Tag, push image
```bash
docker tag kubeapp <username>/k8sapp
docker push <username>/k8sapp
```

#### 3. Deploy, creating RC
``` bash
kubectl run k8sapp --image=user/imagename --port=8080 --generator=run/v1
```

#### 4. Create a service
```bash
kubectl expose rc k8sapp --type=LoadBalancer --name=k8sapp-http
```

#### 5.  If you'tre using minikube for Kubernetes cluster run
```bash
minikube service k8sapp-http
```

#### 6. Scale
```bash
kubectl scale rc k8sapp --replicas=3
```

#### 7. View dashboard
``` ash
minikube service kubernetes-dashboard -n kube-system  
```
