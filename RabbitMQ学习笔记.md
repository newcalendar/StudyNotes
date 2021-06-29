## RabbitMQ学习笔记

## 一、MQ基本概念

1、MQ指定是消息队列，是在消息传输过程中保存信息的容器。

2、MQ的优势和缺点

优点

（1）应用解耦：增加容错性和可扩展、维护性

（2）异步提速

（3）削峰填谷：提高系统稳定性

缺点：

(1)MQ可用性降低

(2)系统复杂度提高

(3)一致性问题

3、使用MQ的时机：

（1）生产者不需要得到消费者的反馈

（2）允许短暂的不一致性

（3）比使用前更有效果

4、常用的MQ

1、RabbitMQ 、RocketMQ、ActiveMQ、kafka、ZeroMQ、MetaMQ,借用Redis充当消息队列

## 二、RabbitMQ

1、基于AMQP高级消息队列协议网络协议，使用Erlang语言开发。

### 一、管理后台

1、Overview 当前消息信息、节点信息、端口信息、导入导出配置文件

2、Connections

3、Channels

4、Exchanges

5、Queues

6、Admin 添加用户、添加虚拟机、添加策略



### 二、快速入门





