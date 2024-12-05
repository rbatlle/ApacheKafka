# Apache Kafka - MQ Broker

### Install Java package

```
[root@localhost ~] yum install java-1.8.0-openjdk-devel
```

### Configure Java Home

```
advertises --config java
```

### Edit file .bashrc on path ~ by adding Java home path

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.432.b06-3.0.1.el9.x86_64/jre         
export PATH=$PATH:$JAVA_HOME/bin
```

### Check changes are made

```
[root@localhost ~]# source ~/.bashrc 
[root@localhost ~]# echo $JAVA_HOME
```

### Download Apache Kafka from official repository

```
wget https://dlcdn.apache.org/kafka/3.9.0/kafka_2.13-3.9.0.tgz
```
```
tar -xzvf kafka_2.13-3.9.0.tgz
```

### Enter inside kafka directory and /bin folder

```
cd kafka_2.13-3.9.0
```

```
cd /bin
```





