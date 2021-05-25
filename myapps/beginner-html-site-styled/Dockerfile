FROM oraclelinux:8.3 
# Base OS image from Dockerhub 
MAINTAINER ashutoshh@linux.com
RUN dnf install httpd -y
# way to install httpd server in OL 
WORKDIR /var/www/html/
# is to change directory during image build time
COPY  ./beginner-html-site-styled-gh-pages   .
# first . means source and last  . means target 
CMD  ["httpd","-DFOREGROUND"]
#  default parent process 
# its a script to start httpd web server 