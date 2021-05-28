# stage 1 just build project into war 
FROM  oraclelinux:8.3  as Builder
MAINTAINER  ashutoshh@linux.com
# Install jdk 8 
RUN  dnf install java-1.8.0-openjdk.x86_64 -y
# INstalling maven 
RUN  dnf  install maven -y
# creating direcoty 
RUN mkdir /javawebapp
ADD .  /javawebapp/
#  running  maven to convert into .war 
# changing directory 
WORKDIR  /javawebapp
# building war file 
RUN  mvn clean package 
# if mvn clean step successfully happen ---      .war file will be create 

# Stage 2 here we will deploy war file into tomcat 
FROM  tomcat
MAINTAINER  ashutoshhsingh93@gmail.com
RUN mkdir /tmpcode
#  copy a directory data from builder stage to final 
COPY  --from=Builder  /javawebapp  /tmpcode
RUN cp -rvf  /javawebapp/target/WebApp.war  /usr/local/tomcat/webapps/
RUN rm -rvf  /tmpcode/ 
EXPOSE 8080
