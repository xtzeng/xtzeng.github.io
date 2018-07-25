---
title: rabbitMQ中的几个概念
date: 2018-06-13 13:27:10
tags: [rabbitMQ]
---

 	producer：消息生产者

    consumer：消息消费者

    virtual host：虚拟主机，在RabbitMQ中，用户只能在虚拟主机的层面上进行一些权限设置，比如我可以访问哪些队列，我可以处理哪些请求等等；

    broker：消息转发者，也就是我们RabbitMQ服务端充当的功能了，那么消息是按照什么规则进行转发的呢？需要用到下面几个概念；

    exchange：交换机，他是和producer直接进行打交道的，有点类似于路由器的功能，主要就是进行转发操作的呗，那么producer到底用哪个exchange进行路由呢？这个取决于routing key(路由键)，每个消息都有这个键，我们也可以自己设定，其实就是一字符串；

    queue：消息队列，用于存放消息，他接收exchange路由过来的消息，我们可以对队列内容进行持久化操作，那么queue到底接收那个exchange路由的消息呢？这个时候就要用到binding key(绑定键)了，绑定键会将队列和exchange进行绑定

