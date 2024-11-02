



```bash
#HBASE CONFIGS
export HBASE_HOME="/usr/local/hbase"
export PATH="$HBASE_HOME/bin:$PATH"
```


`sudo nano /usr/local/hbase/conf/hbase-env.sh`

```bash
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
export HBASE_PID_DIR=/var/hbase/pids
export HBASE_MANAGES_ZK=false
export HBASE_DISABLE_HADOOP_CLASSPATH_LOOKUP="true"
```




sudo chmod 777 /usr/local/hbase
sudo chmod 777 /usr/local/hbase/
sudo chmod 777 /usr/local/hbase/*
sudo chmod 777 /var
sudo chmod 777 /var/
sudo chmod 777 /var/*