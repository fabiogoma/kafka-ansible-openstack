# README.md still under development

# What?
In this project you will find infrastructure as code to provision from the scratch a new environment for a kafka cluster.

# Used tools
The used tools for this solution are mainly open source, you can check the list below:
OpenStack
CentOS (OS on the OpenStack cloud)
Fedora (OS on my personal laptop)
Vagrant
Ansible
Zookeeper
Kafka
mDNS (Avahi Daemon)

# How?
For now, this project work only on Linux machines, feel free to port it to any other platform.

### Step 1 - Install
Make sure that you have installed on your laptop the Vagrant and its OpenStack provider

### Step 2 - Clone
Now you can clone my repo and take a look on the Vagrant file available on your root directory. As you can see the password is an external variable, so make sure you have that variable exported on your terminal

### Step 3 - Run
You are now able to bring up your environment, by just typing $ vagrant up

### Step 4 - Test
Now that your environment is UP and Running, you can do a test.
In order to execute the test, get Kafka tarball on the same version used on my project. Explode it in any folder you like, then open two terminals.

First Terminal
```console
./kafka-topics.sh --create --topic MyTopic --replication-factor 1 --partitions 1 --zookeeper zookeeper1.local:2181,zookeeper2.local:2181,zookeeper3.local:2181  

./kafka-console-producer.sh --broker-list kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```
Here, type some "Hello World" messages, then open a second terminal to consume those messages.

Second Terminal
```console
./kafka-console-consumer.sh --bootstrap-server kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```

Keep in mind that this is my personal laboratory, you can prepare you're production environment following this steps, but make sure you know what you're doing.
