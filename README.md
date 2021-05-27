# Day3 overall summary 

<img src="rev.png">

## checking connection 

```
❯ kubectl   get   nodes
NAME         STATUS   ROLES                  AGE   VERSION
masternode   Ready    control-plane,master   25h   v1.21.1
minion1      Ready    <none>                 25h   v1.21.1
minion2      Ready    <none>                 25h   v1.21.1
minion3      Ready    <none>                 25h   v1.21.1
```


## checking number of pods 

```
❯ kubectl  get  pods
NAME           READY   STATUS    RESTARTS   AGE
ajitpod-123    1/1     Running   1          16h
ashupod-123    1/1     Running   1          16h
asimpod-123    1/1     Running   1          16h
ganesh-123     1/1     Running   1          16h
narsing-123    1/1     Running   1          16h
priyapod-123   1/1     Running   1          16h
rahulpod-123   1/1     Running   1          16h
shobhit-pod    1/1     Running   1          16h
sudhi-pod1     1/1     Running   1          16h

```

## Deleting pods 

```
❯ kubectl  delete  po   ashupod-123
pod "ashupod-123" deleted
```

## namespace introduction. 

<img src="ns.png">

## list of namespaces

```
❯ kubectl   get  ns
NAME                   STATUS   AGE
default                Active   25h
delvex                 Active   101m
ingress-nginx          Active   25h
kube-node-lease        Active   25h
kube-public            Active   25h
kube-system            Active   25h
kubernetes-dashboard   Active   16h
new                    Active   130m
oracle                 Active   25h
```

###. default namespaces 

<img src="ksns.png">

## checking kube-system namespace 

<img src="kubes.png">

## creating namespace 

```
❯ kubectl  create   namespace   ashuproject1
namespace/ashuproject1 created
❯ kubectl  get  ns
NAME                   STATUS   AGE
ashuproject1           Active   5s
default                Active   25h

```

## chaning default namespace 

```
❯ kubectl   get   po
No resources found in default namespace.
❯ kubectl  config  set-context --current  --namespace=ashuproject1
Context "kubernetes-admin@kubernetes" modified.
❯ kubectl   get   po
No resources found in ashuproject1 namespace.

```

### deploy pod 

```
❯ kubectl  apply -f  ashupod1.yaml
pod/ashupod-123 created
❯ kubectl  get  po
NAME          READY   STATUS    RESTARTS   AGE
ashupod-123   1/1     Running   0          13s
❯ kubectl  get  po
NAME          READY   STATUS    RESTARTS   AGE
ashupod-123   1/1     Running   0          53s
❯ kubectl  get  po -o wide
NAME          READY   STATUS    RESTARTS   AGE   IP               NODE      NOMINATED NODE   READINESS GATES
ashupod-123   1/1     Running   0          62s   192.168.50.205   minion3   <none>           <none>


```

## checking current namespace 

```
❯ kubectl  get  po
NAME          READY   STATUS    RESTARTS   AGE
ashupod-123   1/1     Running   0          10m
❯ kubectl  config  get-contexts
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashuproject1


```


## auto-generating yaml for POD

```
10005  kubectl  run   ashupod-2   --image=dockerashu/httpd:25thmay2021v1  --port=80  --dry-run=client 
10006  kubectl  run   ashupod-2   --image=dockerashu/httpd:25thmay2021v1  --port=80  --dry-run=client  -o yaml 
10007  cd  Desktop/myapps/Pod
10008  ls
10009  kubectl  run   ashupod-2   --image=dockerashu/httpd:25thmay2021v1  --port=80  --dry-run=client  -o yaml  >abc.yml
10010  ls

```

# accessing pod app from k8s client machine 

```
❯ kubectl  port-forward   ashupod-2    1234:80
Forwarding from 127.0.0.1:1234 -> 80
Forwarding from [::1]:1234 -> 80
Handling connection for 1234
Handling connection for 1234

```


## access info 

<img src="net1.png">



