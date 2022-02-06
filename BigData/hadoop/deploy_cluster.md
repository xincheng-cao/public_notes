# master/slave1/slave2

## java
sudo apt install openjdk-8-jdk

## pdsh
sudo apt-get update

sudo apt-get install pdsh

## hadoop
wget https://dlcdn.apache.org/hadoop/common/stable/hadoop-3.3.1.tar.gz

tar -xvf hadoop-3.3.1.tar.gz

mv hadoop-3.3.1 hadoop

## .bashrc
nano .bashrc

export PDSH_RCMD_TYPE=ssh

##  hadoop-env.sh

vim ~/hadoop/etc/hadoop/hadoop-env.sh

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/

## mv
sudo mv hadoop /usr/local/hadoop

## /etc/environment

sudo vim /etc/environment

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/hadoop/bin:/usr/local/hadoop/sbin"

JAVA_HOME="/home/ubuntu/jdk-11.0.2/jre"

## add user
sudo adduser hadoopuser

p hadoopuser

sudo usermod -aG hadoopuser hadoopuser
sudo chown hadoopuser:root -R /usr/local/hadoop/
sudo chmod g+rwx -R /usr/local/hadoop/
sudo adduser hadoopuser sudo


## confirm ip addr for master and slaves
ip addr

master: 172.31.16.179

slave1: 172.31.29.202

slave2: 172.31.24.146

## /etc/hosts
sudo vim /etc/hosts

172.31.16.179 hadoop-master
172.31.29.202 hadoop-slave1
172.31.24.146 hadoop-slave2

## /etc/hostname

sudo nano /etc/hostname

`hadoop-master` on master node
`hadoop-slave1` on slave node 1
`hadoop-slave2` on slave node 2

sudo reboot

## ssh
sudo vim /etc/ssh/sshd_config

PasswordAuthentication yes

sudo reboot

# master

## ssh
su - hadoopuser

ssh-keygen -t rsa

ssh-copy-id hadoopuser@hadoop-master
ssh-copy-id hadoopuser@hadoop-slave1
ssh-copy-id hadoopuser@hadoop-slave2