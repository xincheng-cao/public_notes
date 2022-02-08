# deploy spark on yarn cluster

## master

### download

cd ~

wget https://dlcdn.apache.org/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz

tar -xvf spark-3.2.1-bin-hadoop3.2.tgz

mv spark-3.2.1-bin-hadoop3.2 spark

### ~/.profile

vim ~/.profile

PATH=/home/hadoopuser/spark/bin:$PATH

### integrate with yarn

vim ~/.profile

export SPARK_HOME=/home/hadoopuser/spark
export LD_LIBRARY_PATH=/usr/local/hadoop/lib/native:$LD_LIBRARY_PATH

re-login

### spark-defaults.conf

mv $SPARK_HOME/conf/spark-defaults.conf.template $SPARK_HOME/conf/spark-defaults.conf

vim spark-defaults.conf

spark.master    yarn
spark.driver.memory    7g