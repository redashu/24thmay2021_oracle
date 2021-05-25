FROM oraclelinux:8.3  
# choosing base image using FROM instruction 
# this image will be pulled / downloaded from Dockerhub 
MAINTAINER  ashutoshh@linux.com 
ENV x=2 
# it is creating an ENV variable inside your docker image 
# and that will be available in container also 
# just optional keyword but you can share image owner details
# for any assistance 
RUN  dnf  install python3 -y
# RUN is to execute any command or script 
RUN mkdir  /ashu
# creating a directory 
COPY  oracle.py  /ashu/oracle.py
ADD   hello.py  /ashu/hello.py
WORKDIR  /ashu/
# copy -- is to copy data from client machine 
# to docker engine during image build time
#CMD ["python3","/ashu/hello.py"]
ENTRYPOINT  ["python3"]
CMD ["hello.py"]
#  this is for default parent proces
#docker  run -itd --name c1  ashu:pyv1   
#docker  run -itd --name c2 ashu:pyv1 oracle.py



