FROM jenkins/jenkins:latest
MAINTAINER symbolspace <symbolspace@outlook.com>

# replace update center url, from https://github.com/symbolspace/jenkins-dotnet/raw/master/compose/data/home/hudson.model.UpdateCenter.xml
RUN  echo "<?xml version='1.1' encoding='UTF-8'?>" > /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "<sites>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "  <site>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "    <id>default</id>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "    <url>https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json</url>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "  </site>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml \
  && echo "</sites>" >> /var/jenkins_home/hudson.model.UpdateCenter.xml

# set time zone
ENV TZ=Asia/Shanghai

# using user: root
USER root

# using 163 mirrors
RUN  cp /etc/apt/sources.list /etc/apt/sources.list.bak \
   && echo "deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib" > /etc/apt/sources.list \
   && echo "deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib" >> /etc/apt/sources.list \
   && apt-get update

# set dotnet repo
RUN  wget --no-check-certificate --no-cookies -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /microsoft.asc.gpg \
   && mv /microsoft.asc.gpg /etc/apt/trusted.gpg.d/ \
   && wget --no-check-certificate --no-cookies -O /etc/apt/sources.list.d/microsoft-prod.list https://packages.microsoft.com/config/debian/10/prod.list \
   && chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg \
   && chown root:root /etc/apt/sources.list.d/microsoft-prod.list \
   && apt-get update \
   && apt-get install apt-transport-https \
   && apt-get update
   
# install dotnet core
RUN   apt-get install dotnet-sdk-3.1 -y \
   && apt-get install aspnetcore-runtime-3.1 -y \
   && apt-get install dotnet-sdk-2.2 -y \
   && apt-get install aspnetcore-runtime-2.2 -y

# restore sources to default
RUN \cp  /etc/apt/sources.list.old /etc/apt/sources.list

# restore user: jenkins
USER jenkins
