# kafka 使用

### 1、安装
macOS
```bash
$ brew install kafka
```

### 2、运行服务
macOS
```bash
$ brew services start kafka
```

### 3、新建topic
```bash
$ kafka-topics --create --topic=hello --zookeeper=localhost:2181 --partitions=1 --replication-factor=1
```


### c++ example
```bash
$ git clone https://github.com/mfontanini/cppkafka
```


### 别的操作被人问到了再写……

