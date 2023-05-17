## Chapter 7

###### Passing configuration and sensitive information to containters
#### 1. Create a fortune script:
```shell
$INTERVAL=$1
echo configuration to generate new fortune every $INTERVAL seconds
mkdir -p /var/htdocs
while :
do 
    echo $(date) Writing fortune to /var/htdocs/index.html 
    /usr/games/fortune > /var/htdocs/index.html
    sleep $INTERVAL
done
```

<br>

#### 2. Dockerfile:
> you can change the based image
```dockerfile
FROM ubuntu:latest

RUN apt-get update ; apt-get -y install fortune
ADD fortuneloop.sh /bin/fortuneloop.sh

ENTRYPOINT ["/bin/fortuneloop.sh"]
CMD ["10"]
```

<br>

#### 3. Build image:
```shell
docker build -t <your_name>/fortune:args .
```

<br>

#### 4. Push the docker image:
```shell
docker push <your_name>/fortune:args 
``` 

<br>

#### 5. Test the docker image:
```console
docker run -it <your_name>/fortune:args | Configured to generate new fortune every 10 seconds
```

<br>

#### 6. Create `.yaml` file:
```yaml
---
apiVersion: v1
kind: Pod
metadata: 
  name: fortune2s
spec:
  containers:
  - image: evalle/fortune:args
    args: ["2"]
    name: html-generator
    volumeMounts:
    - name: html 
      mountPath: /var/htdocs
  - image: nginx:alpine
    name: web-server
    volumeMounts:
    - name: html
      mountPath: /usr/share/nginx/html
      readOnly: true
    ports:
    - containerPort: 80
      protocol: TCP
  volumes:
  - name: html
    emptyDir: {}
```

<br>

#### 7. Create a kubernetes pod from the yaml file:
```bash
kubectl create -f fortune2s.yaml
```

