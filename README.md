# README.md still under development

### First Terminal
```console
./kafka-topics.sh --create --topic MyTopic --replication-factor 1 --partitions 1 --zookeeper zookeeper1.local:2181,zookeeper2.local:2181,zookeeper3.local:2181  

./kafka-console-producer.sh --broker-list kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```
Here, type some "Hello World" messages, then open a second terminal to consume those messages.


### Second Terminal
```console
./kafka-console-consumer.sh --bootstrap-server kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```

Keep in mind that this is my personal laboratory, you can prepare you're production environment following this steps, but make sure you know what you're doing.
