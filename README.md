# Just overview 

<img src="rev.png">


## Deployment ACR image to k8s as POD 

### pushing image to ACR 

```
 docker  tag   nginx:28thmay2021v1    oracleindia.azurecr.io/nginx:28thmay2021v1 
 docker login  oracleindia.azurecr.io
 docker  push  oracleindia.azurecr.io/nginx:28thmay2021v1 
 docker logout oracleindia.azurecr.io
 ```

### deploy pod 

<img src="acrer.png">

## secret understanding 

<img src="secret.png">

## ACR image deployment in k8s

### creating secret 

```
❯ kubectl  create  secret    docker-registry   ashusec  --docker-server=oraclein.azurecr.io  --docker-username=oraclein      --docker-password=pbJxt=N0nVD1FIqpDc -n  ashuproject1
secret/ashusec created
❯ kubectl  get  secret
NAME                  TYPE                                  DATA   AGE
ashusec               kubernetes.io/dockerconfigjson        1      39s
default-token-gb5gm   kubernetes.io/service-account-token   3      24h


```


### node dedploying 

```
❯ kubectl  get  po
NAME             READY   STATUS             RESTARTS   AGE
ashu-rc1-46nk9   1/1     Running            1          17h
ashu-rc1-j8569   1/1     Running            1          18h
ashupod111       0/1     ImagePullBackOff   0          14m
❯ kubectl  replace  -f  ng.yml  --force
pod "ashupod111" deleted
pod/ashupod111 replaced
❯ kubectl  get  po
NAME             READY   STATUS    RESTARTS   AGE
ashu-rc1-46nk9   1/1     Running   1          17h
ashu-rc1-j8569   1/1     Running   1          18h
ashupod111       1/1     Running   0          4s

```

### creating service 

```
kubectl  expose pod  ashupod111  --type NodePort --port 1234 --target-port 80  --name ashuss11 

```

### cleaning up 

```
❯ kubectl  delete  all --all
pod "ashu-rc1-46nk9" deleted
pod "ashu-rc1-j8569" deleted
pod "ashupod111" deleted
replicationcontroller "ashu-rc1" deleted
service "ashuss11" deleted
service "ashusvc099" deleted
service "ashusvc88" deleted

```

## Deployment 


### creating 

```
 kubectl  create  deployment   ashudep111  --image=oracleindia.azurecr.io/nginx:28thmay2021v1  --dry-run=client -o yaml              >deploy1.yml
 
 
```

### creating LB service 

```
 kubectl   create  service  loadbalancer  ashusv443  --tcp  1234:80  --dry-run=client  -o yaml 
 
```
### deploying 

```

❯ kubectl  apply -f  deploy1.yml
deployment.apps/ashudep111 created
service/ashusv443 created
❯ kubectl  get deploy
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashudep111   0/1     1            0           8s
❯ kubectl  get   rs
NAME                    DESIRED   CURRENT   READY   AGE
ashudep111-576f7d58bb   1         1         1       12s
❯ kubectl  get   pod
NAME                          READY   STATUS    RESTARTS   AGE
ashudep111-576f7d58bb-hvgvj   1/1     Running   0          16s
❯ kubectl  get   svc
NAME        TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
ashusv443   LoadBalancer   10.103.135.81   <pending>     1234:30277/TCP   20s

```

### scaling 

```
❯ kubectl  get  deploy
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashudep111   1/1     1            1           7m51s
❯ kubectl  scale  deploy ashudep111  --replicas=5
deployment.apps/ashudep111 scaled
❯ kubectl  get  deploy
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashudep111   1/5     5            1           8m6s
❯ kubectl  get  deploy
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashudep111   5/5     5            5           8m9s

```



