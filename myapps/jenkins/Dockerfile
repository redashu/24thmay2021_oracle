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
CMD  java -jar  jenkins.war

