# Docker
#Descriprion
#Manuals... Dockers... Local dockers...

###----Install local docker----###

#(for MacOS)
docker-machine create -d virtualbox --virtualbox-disk-size "100000" --virtualbox-cpu-count "2" \
--virtualbox-memory "4096" --virtualbox-no-dns-proxy  default
eval $(docker-machine env default)
docker run -d --name testjenkins -v jenkinshome:/var/jenkins_home jenkins/jenkins:2.176.2-jdk11

#.....something plugins......

#copy file configuration bashrc by root to $HOME by Jenkins
cp /root/.bashrc $HOME/

#export jenkins variables to PATH
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$HOME.local/bin
source $PATH

#Install sudo command (optional)
apt-get install sudo -y

#Access credentials for user Jenkins
usermod -aG sudo jenkins

#some parameter for sudo
visudo
#Insert command
jenkins ALL=(ALL) NOPASSWD: ALL


#Additional commands
docker exec -it -u root (ID container) bash

#Backup and restore volumes
______________________________________________________________________________________________________________________

Backup:

docker run --rm --volumes-from testjenkins -v $(echo jhbkp-$(date +"%H-%M-%S_%d-%m-%y")):/var/jenkins_home_bkp ubuntu cvf /backup/backup.tar /var/jenkins_home


______________________________________________________________________________________________________________________

Restore:

docker run -v /var/jenkins_home --name restoretemp ubuntu /bin/bash

1. docker run -d --name testjenkins-1 -p 8081:8080 --mount src=<BKPVOL>,target=/backup jenkins/jenkins:2.176.2-jdk11

2. docker exec -it -u root testjenkins-1 bash -c "tar xvf /backup/backup.tar"
