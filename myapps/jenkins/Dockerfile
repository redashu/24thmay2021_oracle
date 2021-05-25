FROM ubuntu
MAINTAINER  ashutoshh@linux.com
RUN apt  update 
#ARG  DEBIAN_FRONTED=noninteractive
#ENV  TZ=Asia/Kolkata
RUN apt install  tzdata -y
RUN  apt install openjdk-8-jdk wget -y
RUN mkdir  /cicd
WORKDIR  /cicd
RUN wget https://get.jenkins.io/war-stable/2.277.4/jenkins.war
EXPOSE 8080 
# these days this is an optional field 
#CMD  java -jar  jenkins.war
ENTRYPOINT  java -jar  jenkins.war 
# CMD and Entrypoint both are same but 
# parent process by ENTRYPOINT can't be replaced as last argument during docker run
#docker run -itd -name c1  jenkins:tryv1  ping fb.com 

#docker run -itd --name c1 --entrypoint cal    jenkins:tryv1 

