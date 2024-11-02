# STEP 1. set hosts and hostname

`sudo nano /etc/hosts  `

```bash
192.168.10.5 h-primary  
192.168.10.6 h-secondary1
#tambahkan lagi jika butuh
```

`sudo nano /etc/hostname` 
```bash
#namai mesin sesuai dengan yang mau di tetapkan 
#contoh mesin 1 ingin nama 
h-primary

#mesin 2 ingin nama 
h-secondary1
```

## setting ip static 
`sudo nano /etc/netplan/00-installer-config.yaml`

```bash
# This is the network config written by 'subiquity'
# di sini hanya sampel, sesuaikan dengan milik anda
network:
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses:
      - 192.168.10.5/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
        - 8.8.8.8
        - 8.8.4.4
        search: []
  version: 2

```


## install java
  
`sudo apt install openjdk-8-jdk`    
tunggu proses instalasi selesai.    
kemudian check java apakah di kenali    
`java -version`


`sudo nano /etc/environment ` 
```bash
#tambahkan setelah baris PATH
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
```


## membuat user baru 

`sudo adduser h-user`   
`sudo usermod -aG sudo h-user`

masuk ke user yang sudah di buat    
`su - h-user`




## gunakan perintah di bawah ini jika anda sudah clone mesin 

`ssh-keygen -t rsa`

copy key in cluster 

`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@h-primary`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@h-secondary1`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@h-secondary2`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@zookeeper1`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@zookeeper2`  
`ssh-copy-id -i ~/.ssh/id_rsa.pub h-user@zookeeper3`  


