# install and setup hadoop

## 1. download hadoop

`sudo wget -P ~ https://dlcdn.apache.org/hadoop/common/stable/hadoop-3.4.0.tar.gz`


## 2. extract

`tar xzf hadoop-3.4.0.tar.gz`

## 3. move to new folder

`sudo mv hadoop-3.4.0.tar.gz hadoop`

## 4. move to local user 

`sudo mv hadoop /usr/local/hadoop`

## 5. set env hadoop

`nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh`

tambahkan java path 

```bash
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
# tambahkan hal lain jika di butuhkan seperti port ssh custom

```

## 6. add path hadoop

`sudo nano ~/.bashrc`

```bash
#Hadoop Related Options
export HADOOP_HOME="/usr/local/hadoop"
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

terapkan perubahan 
`source ~/.bashrc`

## 7. setting xml hadoop

buka file **CORE** dan **HDFS** saja, kemudian copy pengaturan ke primary saja

setelah selesai 

copy configurasi ke semua cluster 

`scp /usr/local/hadoop/etc/hadoop/* h-secondary1:/usr/local/hadoop/etc/hadoop/`  
`scp /usr/local/hadoop/etc/hadoop/* h-secondary2:/usr/local/hadoop/etc/hadoop/`