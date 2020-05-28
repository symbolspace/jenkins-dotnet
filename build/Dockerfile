FROM jenkins/jenkins:latest
MAINTAINER symbolspace <symbolspace@outlook.com>

RUN  mv /etc/apt/sources.list /etc/apt/sources.list.old \
   && echo "deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib" > /etc/apt/sources.list \
   && echo "deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib" >> /etc/apt/sources.list \
   && echo "deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib" >> /etc/apt/sources.list \
   && apt update
RUN wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg \   
   && mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ \
   && wget https://packages.microsoft.com/config/debian/10/prod.list \
   && mv prod.list /etc/apt/sources.list.d/microsoft-prod.list \
   && chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg \
   && chown root:root /etc/apt/sources.list.d/microsoft-prod.list \
   && apt-get update \
   && apt-get install apt-transport-https \
   && apt-get update \
   && apt-get install dotnet-sdk-3.1 -y \
   && apt-get install aspnetcore-runtime-3.1 -y \
   && apt-get install aspnetcore-runtime-2.2 -y

RUN rm -f /etc/apt/sources.list \
   &&  mv /etc/apt/sources.list.old /etc/apt/sources.list

ENV TZ=Asia/Shanghai
