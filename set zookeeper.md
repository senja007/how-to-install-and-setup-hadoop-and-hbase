# zookeeper cluster


download  
`https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.8.4/apache-zookeeper-3.8.4-bin.tar.gz`

extract

`tar xzf apache-zookeeper-3.8.4-bin.tar.gz`


## pindahkan ke folder baru

`sudo mv apache-zookeeper-3.8.4 zookeeper`

## pindahkan ke dalam user local

`sudo mv apache-zookeeper-3.8.4 /usr/local/zookeeper`


## buat folder penampung

`sudo mkdir -p /usr/local/zookeeper/data`

## tambahkan path 

`sudo nano ~/.bashrc`

```bash
#zookeeper home
export PATH=$PATH:/usr/local/zookeeper/bin
```

`source ~/.bashrc`