# dokumentasi hadoop
## mesin dari server psdku-lumajang

### 1. config port ssh
port ssh menggunakan custom port yaitu 2792

`sudo nano /etc/ssh/sshd_config`

aktifkan port custom dan permitRootLogin no

### 2. buat kunci ssh

`ssh-keygen -t ed25519 -C "" -P ""`

kemudian pindah kunci ke authorized_keys.  
`cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys`

### 3. install java 

`sudo apt install openjdk-8-jdk`

setelah selesai cek silakan cek java  
`java -version`

### 4. download hadoop dan hbase
download hadoop & hbase di sini.

`https://mirrors.sonic.net/apache/hadoop/common/stable/hadoop-3.4.0.tar.gz`

`https://downloads.apache.org/hbase/stable/hbase-2.5.9-bin.tar.gz`

kemudian extrac hadoop yang sudah di download

`tar xzf hadoop-3.4.0.tar.gz`  
`tar xzf hbase-2.5.9-bin.tar.gz`

### 5. move ke folder 
`mv hadoop-3.4.0 hadoop`


### 6. setting hadoop-env.sh
`nano ~/hadoop/etc/hadoop/hadoop-env.sh`  

paste java home dan ssh custom  
`export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/`

`export HADOOP_SSH_OPTS="-p 2792"`  

### 7. move ke dalam local user
`sudo mv hadoop /usr/local/hadoop`  

### 8. tambah java home di env linux
`sudo nano /etc/environment`

```json
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/hadoop/bin:/usr/local/hadoop/sbin"
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
```
### 9. membuat user baru 
`sudo adduser hadoopuser`  

tambahkan permission ke user baru  
`sudo usermod -aG hadoopuser hadoopuser`  
`sudo chown hadoopuser:root -R /usr/local/hadoop/`  
`sudo chmod g+rwx -R /usr/local/hadoop/`  
`sudo adduser hadoopuser sudo`  


### 10. duplikat vm 
sesuai yang di butuhkan  
setelah selesai duplikat pastikan ubah ip jika statik dan hostname  
perintah ubah hostname
`sudo nano /etc/hostname`  
perintah ubah ip  `sudo nano /etc/netplan/00-installer-config.yaml`  
perintah untuk menambah hosts 
`sudo nano /etc/hosts`  
tambahkan hal berikut
```json

#use ip public
#hadoop and hbase
114.9.22.101 h-primary
114.9.22.102 h-secondary1
114.9.22.103 h-secondary2

#zookeeper
114.9.22.104 zookeeper1
114.9.22.105 zookeeper2
114.9.22.106 zookeeper3


#use local
#hadoop and hbase
#192.168.50.10 h-primary
#192.168.50.11 h-secondary1
#192.168.50.12 h-secondary2

#zookeeper
#192.168.50.50 zookeeper1
#192.168.50.51 zookeeper2
#192.168.50.52 zookeeper3
```

### 11. create ssh key di hadoopuser
`ssh-keygen -t rsa`

kemudian bagikan ke yang lain  
`ssh-copy-id -p 2792 hadoopuser@h-primary`  
`ssh-copy-id -p 2792 hadoopuser@h-secondary1`  
`ssh-copy-id -p 2792 hadoopuser@h-secondary2`  
  



## hanya di setting di h-primary
### 12. hadoop core-site.xml
`sudo nano /usr/local/hadoop/etc/hadoop/core-site.xml`  

tambahkan baris berikut
```json
<configuration>
<property>
<name>fs.defaultFS</name>
<value>hdfs://h-primary:6969</value>
</property>
</configuration>
```

atur hdfs-site.xml  
`sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml`
```json
<configuration>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/usr/local/hadoop/data/nameNode</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/usr/local/hadoop/data/dataNode</value>
    </property>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
</configuration>
```

atur workers  
`sudo nano /usr/local/hadoop/etc/hadoop/workers`
```json
h-primary
h-secondary1
h-secondary2
```

### 13. copy ke secondary
copy paste config master ke secondary lain  
`scp -P 2792 /usr/local/hadoop/etc/hadoop/* h-secondary1:/usr/local/hadoop/etc/hadoop/`  
`scp -P 2792 /usr/local/hadoop/etc/hadoop/* h-secondary2:/usr/local/hadoop/etc/hadoop/`


```json

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```



hadoop allow port
```bash
#ufw 
sudo ufw allow outgoing
sudo ufw deny incoming 

#port ssh
sudo ufw allow 

#menyesuaikan port hadoop master




```


`export HBASE_SSH_OPTS="-p 2792"`


```json
sudo chmod 777 /usr/local/hbase
sudo chmod 777 /usr/local/hbase/
sudo chmod 777 /usr/local/hbase/*
sudo chmod 777 /var
sudo chmod 777 /var/
sudo chmod 777 /var/*
```