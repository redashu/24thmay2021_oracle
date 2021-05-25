# Day1 recall

## snap 

<img src="recap.png">

## removing all containers 

```

 docker rm  $(docker ps -aq) 
 
```

## Webapplication containerization 

### webservers 

<img src="webs.png">

## apache httpd webserver

<img src="httpd.png">

## Dockerfile for apache httpd 

<img src="dfile.png">

## Building images 

```
❯ cd beginner-html-site-styled
❯ ls
CODE_OF_CONDUCT.md LICENSE            images             styles
Dockerfile         README.md          index.html
❯ docker  build  -t  httpd:25thmay2021v1  .
Sending build context to Docker daemon  63.49kB
Step 1/6 : FROM oraclelinux:8.3
 ---> 816d99f0bbe8
Step 2/6 : MAINTAINER ashutoshh@linux.com
 ---> Using cache
 ---> af0ac62760ea
Step 3/6 : RUN dnf install httpd -y
 ---> Running in ac7dd4a1aefa


```

### images 

```
❯ docker  images
REPOSITORY    TAG             IMAGE ID       CREATED              SIZE
httpd         shah1           d00966056023   About a minute ago   352MB
httpd         25thmay2021v1   8b0e7be25674   About a minute ago   352MB
httpdasim     training        a3411d2f05e9   2 minutes ago        352MB


```


## image build history 

```
❯ docker  history  8b0e7be25674
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
8b0e7be25674   4 minutes ago   /bin/sh -c #(nop)  CMD ["httpd" "-DFOREGROUN…   0B        
a107416d461f   4 minutes ago   /bin/sh -c #(nop) COPY dir:a10de42d8e22bf749…   57.1kB    
880e35d49aaf   4 minutes ago   /bin/sh -c #(nop) WORKDIR /var/www/html/        0B        
e389d9de2a06   4 minutes ago   /bin/sh -c dnf install httpd -y                 128MB     
af0ac62760ea   18 hours ago    /bin/sh -c #(nop)  MAINTAINER ashutoshh@linu…   0B        
816d99f0bbe8   5 weeks ago     /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B        
<missing>      5 weeks ago     /bin/sh -c #(nop) ADD file:8d6d5e7607cbe7af8…   224MB     

```

### docker run 

```
❯ docker  run -itd --name ashuwebc1  -p  1234:80   httpd:25thmay2021v1
45cfba4274a1752fc9a77a6a2de847ff6ebc6d5fa1cfe458d12c724eae9f9d13

```

### Docker images registry -- Docker hub 

<img src="reg.png">

## docker image name reality 

<img src="imgname.png">

## tagging docker image as your docker user ID before pusing 

```
docker  tag     httpd:25thmay2021v1    dockerashu/httpd:25thmay2021v1
```

### pushing history 

```
10059  docker  tag     httpd:25thmay2021v1    dockerashu/httpd:25thmay2021v1  
10060  docker  images
10061  history
10062  docker  images
❯ docker  login  -u dockerashu
Password: 
Login Succeeded
❯ docker  push  dockerashu/httpd:25thmay2021v1
The push refers to repository [docker.io/dockerashu/httpd]
729ef4f54cc3: Pushed 
9dc80c6bdbab: Pushed 
02a3a073ed48: Mounted from library/oraclelinux 
25thmay2021v1: digest: sha256:a44cfd3acea1810ce3e1a397aceaf2af0600fde185930fa822e31434e5960bf7 size: 950
❯ docker  logout
Removing login credentials for https://index.docker.io/v1/


```




