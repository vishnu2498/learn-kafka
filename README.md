Working of Kafka
-------------------

Kafka is a distributed messaging system/streaming platform.

-------------------------------------------------

Typical Messaging system
------------------------
- Producers 
- Queue
- Consumers

But Kafka is not just another messaging system.

-----------------------------------------------

Working of kafka
--------------------------

1) Kafka is **distributed**? - Kafka works in a cluster, and each node in a cluster is called **BROKER**.
2) Brokers are what makes kafka reliable, scalable and fault-tolerant.

    Kafka Architecture
    -------------------------
   1. In Kafka also, we have producers and consumers.
   2. Instead of a Queue we have **TOPICS**.

--------------------------------------------------------------------------------------------

**TOPICS**
-----------------------
- A topic is divided into partitions. 
- Each topic can have one or more partitions which we specify while creation of the topic.
- If we don't have a key to a message that is published - Kafka handles it in a round robin fashion. (message 1 goes to partition 0, message 2 goes to partition 1 and so on..)
- We can set keys to messages. In that case, messages that share the same key would be sent to the same partition.
- Each message in a partition would receive an offset. Offsets are unique at the partition level. This property makes kafka store messages like a database. We can also recover a message later. That is, it is not immediately deleted unlike other messaging systems.
- Consumers use offsets to read the messages.

--------------------------------------------------------------------------------------------

**BROKERS**
------------------------------------------
kafka works in a distributed way. A kafka cluster may contain many brokers as needed.

- Imagine, kafka as a cluster. Many nodes in the cluster.
- Each node is a broker.
- Each broker is identified by an ID.
- Each broker contains at least one partition of a topic.
- To configure number of partitions in each topic, We need to configure something called **REPLICATION FACTOR** while creating a topic. - for example, if we have a broker with three partitions and a replication factor of three - each broker would be responsible for a partition.
- It is important that the number of partitions match the number of brokers, so each broker would be responsible for a single partition.
- There can ce replicas of a partition is another broker as well. But there is always a Partition leader. the replicas in other brokers will just be in sync. This is helpful when lets say the leader goes down, the data is not lost. It is present in the replicas.

------------------------------------------------------------------------------------------------

Acknowledgement(ack)
----------------
ack is basically a confirmation that the message was delivered from the producer.
Types of Ack 
- ack - 0 -> dont want to receive an ack from kafka. In case of broker failure, message is lost.
- ack - 1 -> receive an ack from only the Partition leader. Data is lost if the leader goes down.
- ack - all -> Most reliable config. Leader and allm its replicas should send ack. This is to ensure that there is no data loss.

-------------------------------------------------------------------------------------

Consumers and Consumer Groups
-----------------------------
- Consumers are applications that are subscribed to a topic.
- It can read from one or more partitions.
- Read is parallel, that is there is no reading order.
- That's why we need to be careful while choosing the number of partitions and while producing the messages.



