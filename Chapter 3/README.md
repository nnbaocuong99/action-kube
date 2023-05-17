## Chapter 3

#### 1. Get `yaml` output (from pod)
```bash
kubectl get po <pod's name> -o yaml
```

<br>

#### 2. Deploy manually:
```bash
$ kubectl create -f nodejs_app.yaml
```

<br>

#### 3. Expose the port 
> ***Warning***: debug only
``` bash
kubectl port-forward kubapp-manual 8888:8080
curl 127.0.0.1:8888
```

<br>

#### 4. Create an app with labels:
```bash
kubectl create -f  nodejs-app-with-labels.yaml
kubectl get po --show-labels
```

<br>

#### 5. Modify label on an existing container
```bash
kubectl label po kubapp-manual creation_method=manual
kubectl label po kubapp-manual-v2 env=debug --overwrite
```

<br>

#### 6. Get namespaces
``` bash
kubectl get ns
```

<br>

#### 7. Create the namespace
```bash
kubectl create -f custom-namespace.yaml
```

<br>

#### 8. Create a resource
```bash
kubectl create -f nodejs_app.yaml --namespace=custom-namespace
kubectl get po --all-namespases
```

<br>

#### 9. Label a node
```bash
kubectl label node minikube --gpu=true
kubectl get nodes -l gpu=true
```

<br>

#### 10. To delete all pods,all
``` bash
kubectl delete po --all | $ kubectl delete all --all
```
