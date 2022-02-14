*[page source](https://medium.com/@jootorres_11979/how-to-set-up-a-hadoop-3-2-1-multi-node-cluster-on-ubuntu-18-04-2-nodes-567ca44a3b12)
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

JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"

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

## core-site.xml
vim /usr/local/hadoop/etc/hadoop/core-site.xml

[example file](./master/core-site.xml)

## hdfs-site.xml
vim /usr/local/hadoop/etc/hadoop/hdfs-site.xml

[example file](./master/hdfs-site.xml)

## workers file
vim /usr/local/hadoop/etc/hadoop/workers

[example file](./master/workers)

## cp to slaves

scp /usr/local/hadoop/etc/hadoop/* hadoop-slave1:/usr/local/hadoop/etc/hadoop/

scp /usr/local/hadoop/etc/hadoop/* hadoop-slave2:/usr/local/hadoop/etc/hadoop/

## format HDFS

source /etc/environment

hdfs namenode -format

## pdsh default rcmd to ssh

vim .bashrc

export PDSH_RCMD_TYPE=ssh

source .bashrc

## start HDFS

start-dfs.sh (login as hadoopuser)

jps (on master and slaves with hadoopuser logged in)

## browser check health

<public_ip>:9870

## configure yarn

vim .bashrc

export HADOOP_HOME="/usr/local/hadoop"
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME

source .bashrc

# Slaves

su - hadoopuser

## yarn-site.xml
vim /usr/local/hadoop/etc/hadoop/yarn-site.xml

[example file](./slaves/yarn-site.xml)

(master node also need to set yarn-site.xml like this)

# Master

su - hadoopuser

## start yarn

start-yarn.sh

## check yarn health

<public_ip>:8088/cluster


# Master and slaves

## update yarn-site.xml on the whole cluster
vim /usr/local/hadoop/etc/hadoop/yarn-site.xml

[master](./master/yarn-site.xml)

[slaves](./slaves/yarn-site.xml)