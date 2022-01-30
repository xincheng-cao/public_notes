# ubuntu

## java

wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz

tar -xvf  openjdk-11.0.2_linux-x64_bin.tar.gz

nano .bashrc

`export JAVA_HOME=/home/ubuntu/jdk-11.0.2`

`export PATH=$PATH:$JAVA_HOME/bin`

source .bashrc

## pdsh
sudo apt-get update

sudo apt-get install pdsh

## hadoop
wget https://dlcdn.apache.org/hadoop/common/stable/hadoop-3.3.1.tar.gz

tar -xvf hadoop-3.3.1.tar.gz

cd /etc/profile.d

sudo nano hadoop_config.sh
HADOOP_HOME=/home/ubuntu/hadoop-3.3.1
export HADOOP_HOME

cd (path to hadoop)/etc/hadoop
