# Basic Concept                                

## 1 Message Model

The RocketMQ message model is mainly composed of Producer, Broker and Consumer. The Producer is responsible for producing messages, the Consumer is responsible for consuming messages, and the Broker is responsible for storing messages.     
The Broker corresponds to one server during actual deployment, and each Broker can store messages from multiple topics, and messages from each Topic can be stored in a different Broker by sharding strategy.     
The Message Queue is used to store physical offsets of messages, and the Message addresses in multiple Topic are stored in multiple Message queues. The Consumer Group consists of multiple Consumer instances.    
##  2 Producer    
The Producer is responsible for producing messages, typically by business systems. It sends messages generated by the business application systems to brokers. The RocketMQ provides multiple paradigms of sending: synchronous, asynchronous,sequential and one-way. Both synchronous and asynchronous methods require the Broker to return confirmation information, while one-way sending is not required.
## 3 Consumer
 The Consumer is responsible for consuming messages, typically the background system is responsible for asynchronous consumption. The Consumer pulls messages from brokers and feeds them into application. In perspective of user application, two types of consumers are provided:Pull Consumer and Push Consumer.
## 4 Topic
The Topic refers to a collection of one kind message. Each topic contains several messages and one message can only belong to one topic. The Topic is the basic unit of RocketMQ for message subscription.
## 5 Broker Server
As the role of the transfer station, the Broker Server stores, and forwards messages. In the RocketMQ system, the Broker Server is responsible for receiving messages sent from producers, storing them and preparing to handle pull requests. It also stores message related meta data, including consumer groups, consuming progress, topics and queues info.
## 6 Name Server
The Name Server serves as the provider of routing service. The Producer or Consumer can find the list of Broker IP addresses corresponding each topic through name server. Multiple Name Servers can be deployed as a cluster, but are independent of each other and do not exchange information.
## 7 Pull Consumer
 A type of Consumer. Applications are usually pulls messages from brokers by actively calling the Consumer's pull message method, and the application has the advantages of controlling the timing and frequency of pulling messages. Once batches of messages are pulled, user application initiates consuming process.                    
## 8 Push Consumer
 A type of Consumer. Under this mode, after the Broker receives the data, it will actively push it to the consumer, which is generally of high real-time performance.                       
## 9 Producer Group
  A collection of the same type of Producer, which sends the same type of messages with consistent logic. If a transaction message is sent and the original producer crashes after sending, the Broker Server will contacts other Producer in the same Producer group to commit or rollback the transactional message.
## 10 Consumer Group
  A collection of the same type of Consumer, which sends the same type of messages with consistent logic. The Consumer Group makes load-balance and fault-tolerance super easy in terms of message consuming.
Warning: consumer instances of one consumer group must have exactly the same topic subscription(s).   

RocketMQ supports two type of consumption mode:Clustering and Broadcasting.
## 11 Consumption Mode - Clustering
Under the Clustering mode, all messages from one topic will be delivered to all consumer instances averagely as much as possible. That is, one message can be consumed by only one consumer instance.
## 12 Consumption Mode - Broadcasting
Under the Broadcasting mode, each Consumer instance of the same Consumer Group receives every message that published to the corresponding topic.
## 13 Normal Ordered Message
Under the Normal Ordered Message mode, the messages received by consumers from the same ConsumeQueue are sequential, while the messages received from different message queues may be non-sequential.
## 14 Strictly Ordered Message
Under the Strictly Ordered Message mode, all messages received by the consumers from the same topic are sequential, as the order they were stored.
## 15 Message
The physical carrier of information transmitted by a messaging system, the smallest unit of production and consumption data, each message must belong to a topic.
Each Message in RocketMQ has a unique Message ID and can carry a key, generally used to store business-related value. The system provides the function to query messages by Message ID and Key.
## 16 Tag
 Flags set for messages to distinguish different types of messages under the same topic, functioning as a "sub-topic". Messages from the same business unit can set different tags under the same topic in terms of different business purposes. The Tag can effectively maintain the clarity and consistency of the code and optimize the query system provided by RocketMQ. The Consumer can realize different "sub-topic" by using Tag, so as to achieve better expansibility.
