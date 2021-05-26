# Docker & containers overview 

<img src="dc.png">

## Remove docker engine with ssh as context 

<img src="context1.png">

### Demo of mac os with Linux DE

<img src="context2.png">

```

docker  context  create  secureaws   --docker  "host=ssh://test1@52.21.252.231" 

```

# Storage for a container 

<img src="cont.png">

## containers are ephemral in nature 

```
[root@ip-172-31-70-148 ~]# docker  exec -it  ashuc1  bash 
[root@250b7445acfc /]# 
[root@250b7445acfc /]# 
[root@250b7445acfc /]# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@250b7445acfc /]# mkdir  hellodata
[root@250b7445acfc /]# ls
bin  boot  dev  etc  hellodata  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@250b7445acfc /]# exit
exit
[root@ip-172-31-70-148 ~]# docker  rm  ashuc1  -f
ashuc1
[root@ip-172-31-70-148 ~]# docker  ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@ip-172-31-70-148 ~]# docker run -itd --name   ashuc1  oraclelinux:8.3 
55bfc14ff2203f9d63778d42d640e836507cdefc7c86cee4e1dbb0ed305aad1a
[root@ip-172-31-70-148 ~]# 
[root@ip-172-31-70-148 ~]# docker  exec -it  ashuc1  bash 
[root@55bfc14ff220 /]# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@55bfc14ff220 /]# exit

```


## Creating docker volumes 

```
[root@ip-172-31-70-148 ~]# docker  volume  create  ashuvol1
ashuvol1
[root@ip-172-31-70-148 ~]# docker  volume  ls
DRIVER    VOLUME NAME
local     ashuvol1
[root@ip-172-31-70-148 ~]# docker  volume  ls
DRIVER    VOLUME NAME
local     ashuvol1
local     rahul1
local     shobhitv1
local     sreevol1
[root@ip-172-31-70-148 ~]# docker  volume  inspect  ashuvol1
[
    {
        "CreatedAt": "2021-05-26T05:24:14Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/mnt/oracle/volumes/ashuvol1/_data",
        "Name": "ashuvol1",
        "Options": {},
        "Scope": "local"
    }
]

```

### more options to DE storage

<img src="engst.png">

```
[root@ip-172-31-70-148 ~]# docker  run -itd --name ashuc2  -v  ashuvol1:/mnt/xyz:rw   alpine ping fb.com 
62e1001f947a2efb180fbd19bb618fba70a5aedca2f9117f8f37dfb2a6dd01fd
[root@ip-172-31-70-148 ~]# 
[root@ip-172-31-70-148 ~]# 
[root@ip-172-31-70-148 ~]# docker  ps
CONTAINER ID   IMAGE             COMMAND             CREATED          STATUS          PORTS     NAMES
83cc4bfcb39f   alpine            "ping google.com"   5 seconds ago    Up 2 seconds              sree_c2_volume
62e1001f947a   alpine            "ping fb.com"       9 seconds ago    Up 7 seconds              ashuc2
4f93196f5d63   alpine            "ping fb.com"       24 seconds ago   Up 20 seconds             asimvolc1
5ead3ce5fd26   oraclelinux:8.3   "/bin/bash"         13 minutes ago   Up 12 minutes             sreec1
55bfc14ff220   oraclelinux:8.3   "/bin/bash"         14 minutes ago   Up 14 minutes             ashuc1
[root@ip-172-31-70-148 ~]# docker  inspect   ashuc2 
[
    {
        "Id": "62e1001f947a2efb180fbd19bb618fba70a5aedca2f9117f8f37dfb2a6dd01fd",
        "Created": "2021-05-26T05:35:35.671691461Z",
        "Path": "ping",
        "Args": [
            "fb.com"
        ],
        "State": {

```

## volume 

```
[root@ip-172-31-70-148 ~]# docker  exec  -it  ashuc2  sh 
/ # cd  /mnt/xyz/
/mnt/xyz # ls
/mnt/xyz # ls
/mnt/xyz # mkdir  hello world
/mnt/xyz # ls
hello  world
/mnt/xyz # exit
[root@ip-172-31-70-148 ~]# docker  rm  ashuc2 -f
ashuc2
[root@ip-172-31-70-148 ~]# docker run -it --rm   -v  ashuvol1:/test:ro  oraclelinux:8.3  bash 
[root@1fc73733bb3d /]# cd  /test/
[root@1fc73733bb3d test]# ls
hello  world
[root@1fc73733bb3d test]# mkdir fine
mkdir: cannot create directory 'fine': Read-only file system
[root@1fc73733bb3d test]# rmdir hello 
rmdir: failed to remove 'hello': Read-only file system
[root@1fc73733bb3d test]# 

```

### on docker engine 

```
[root@ip-172-31-70-148 ~]# cd /mnt/oracle/
[root@ip-172-31-70-148 oracle]# ls
buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
[root@ip-172-31-70-148 oracle]# cd volumes/
[root@ip-172-31-70-148 volumes]# ls
ajitvol1  ashuvol1  asimvol1  backingFsBlockDev  ganesh-volume  metadata.db  narsing_vol1  priyav1  rahul1  shobhitv1  sreevol1  sudhirvol
[root@ip-172-31-70-148 volumes]# cd  narsing_vol1/
[root@ip-172-31-70-148 narsing_vol1]# ls
_data
[root@ip-172-31-70-148 narsing_vol1]# cd _data/
[root@ip-172-31-70-148 _data]# ls
a[1..100]
[root@ip-172-31-70-148 _data]# cd  ..
[root@ip-172-31-70-148 narsing_vol1]# ls
_data
[root@ip-172-31-70-148 narsing_vol1]# cd ..
[root@ip-172-31-70-148 volumes]# cd  ashuvol1/_data/
[root@ip-172-31-70-148 _data]# ls
hello  world
[root@ip-172-31-70-148 _data]# 

```





