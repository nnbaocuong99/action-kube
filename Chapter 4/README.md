## Chapter 4

#### 1. Create the RC
```bash
kubectl create -f k8sapp-rc.yaml
```

<br>


#### 2. To add, remove labels from the scope (pod)
``` bash
$ kubectl label pod <pods name> type=special
$ kubectl label pod <pods name> app=kubapp2 --overwrite
$ kubectl get po
```

<br>

#### 3. To scale RC
```shell
kubectl scale rc k8sapp --replicas=10
```

<br>

#### 4. To delete the RC without pods
```shell
kubectl delete rc k8sapp --cascade=false
```

<br>

5. Start a new RS
```bash
kubectl create -f k8sapp-rs.yaml
```

<br>

#### 6. To check the information about your ReplicaSet run:
```bash
kubectl describe rs
```

<br>

#### 7. Example of scheduled job:
```yaml 
apiVersion: batch/v2alpha1
kind: CronJob
spec:
  schedule: "0 3 * * *"
  startingDeadlineSeconds: 15
```

