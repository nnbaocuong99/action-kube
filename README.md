###### Examples from ["Kubernetes in Action"](https://www.manning.com/books/kubernetes-in-action) by Marko Luksa

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
