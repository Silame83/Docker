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

#Install sudo command (optional)
apt-get install sudo -y

#Access credentials for user Jenkins
usermod -aG sudo jenkins

#some parameter for sudo
visudo
#Insert command
jenkins ALL=(ALL) NOPASSWD: ALL