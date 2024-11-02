# setting firewall ufw 
1. perintah pertama   
```bash
#mengatur ufw keluar masuk data
sudo ufw default deny incoming
sudo ufw default allow outgoing

#port ssh default
sudo ufw allow 22/tcp

#port hadoop master
sudo ufw allow 9000/tcp   


sudo ufw allow 9864:9869/tcp    

#port yarn
sudo ufw allow 8030:8033/tcp


sudo ufw allow 50100/tcp
sudo ufw allow 50105/tcp

#port hbase
sudo ufw allow 16000/tcp
sudo ufw allow 16010/tcp
sudo ufw allow 16020/tcp
sudo ufw allow 16030/tcp

#port zookeeper
sudo ufw allow 2181/tcp

#port web ui hdfs
sudo ufw allow 9870/tcp

#port web ui yarn 
sudo ufw allow 8088/tcp


#port zookeeper
sudo ufw allow 2181/tcp
sudo ufw allow 2888/tcp
sudo ufw allow 3888/tcp


```

sudo ufw enable

2. tambahkan ssh  
`sudo ufw allow 2792/tcp`

3. 



```json
ssh port
6969 #default 22

hadoop master 
6969  #default 9000 

hadoop cluster
9864
9866
9867
9868
9870

```