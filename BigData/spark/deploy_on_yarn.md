# deploy spark on yarn cluster

## master

### download

cd ~

wget https://dlcdn.apache.org/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz

tar -xvf spark-3.2.1-bin-hadoop3.2.tgz

mv spark-3.2.1-bin-hadoop3.2 spark

### ~/.profile

vim ~/.profile

export PATH=/home/hadoopuser/spark/bin:$PATH

### integrate with yarn

vim ~/.profile

export SPARK_HOME=/home/hadoopuser/spark
export LD_LIBRARY_PATH=/usr/local/hadoop/lib/native:$LD_LIBRARY_PATH
export PATH=$PATH:$SPARK_HOME/python
export PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.9.3-src.zip:$PYTHONPATH

re-login

### spark-defaults.conf

mv $SPARK_HOME/conf/spark-defaults.conf.template $SPARK_HOME/conf/spark-defaults.conf

vim spark-defaults.conf

spark.master    yarn
spark.driver.memory    7g
spark.executor.memory     7g

spark.eventLog.enabled  true
spark.eventLog.dir hdfs://hadoop-master:9000/spark-logs

spark.history.provider            org.apache.spark.deploy.history.FsHistoryProvider
spark.history.fs.logDirectory     hdfs://hadoop-master:9000/spark-logs
spark.history.fs.update.interval  10s
spark.history.ui.port             18080

### start spark history_server

hdfs dfs -mkdir /spark-logs

$SPARK_HOME/sbin/start-history-server.sh


### spark.yarn.archive

jar cv0f spark-libs.jar -C $SPARK_HOME/jars/ .

hdfs dfs -mkdir /spark_yarn_archive

hdfs dfs -put spark-libs.jar /spark_yarn_archive

### update spark-defaults.conf

vim spark-defaults.conf

spark.yarn.archive  hdfs://hadoop-master:9000/spark_yarn_archive/spark-libs.jar