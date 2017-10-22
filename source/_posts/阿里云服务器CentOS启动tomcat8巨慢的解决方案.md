---
title: 阿里云服务器CentOS启动tomcat8巨慢的解决方案
date: 2017-10-10 17:29:11
tags: [centos]
---

摘要： 自己再阿里云申请了一台1G1核的机器，每次重启自己的服务tomcat都需要卡住很长时间 经过在网上搜索，找到了原因： Tomcat 7/8都使用org.apache.catalina.util.SessionIdGeneratorBase.createSecureRandom类产生安全随机类SecureRandom的实例作为会话ID，这里花去了342秒，也即接近6分钟。

自己再阿里云申请了一台1G1核的机器，每次重启自己的服务tomcat都需要卡住很长时间
经过在网上搜索，找到了原因：

Tomcat 7/8都使用org.apache.catalina.util.SessionIdGeneratorBase.createSecureRandom类产生安全随机类SecureRandom的实例作为会话ID，这里花去了342秒，也即接近6分钟。

SHA1PRNG算法是基于SHA-1算法实现且保密性较强的伪随机数生成器。

在SHA1PRNG中，有一个种子产生器，它根据配置执行各种操作。

1）如果Java.security.egd属性或securerandom.source属性指定的是”file:/dev/random”或”file:/dev/urandom”，那么JVM会使用本地种子产生器NativeSeedGenerator，它会调用super()方法，即调用SeedGenerator.URLSeedGenerator(/dev/random)方法进行初始化。

2）如果java.security.egd属性或securerandom.source属性指定的是其它已存在的URL，那么会调用SeedGenerator.URLSeedGenerator(url)方法进行初始化。

这就是为什么我们设置值为”file:///dev/urandom”或者值为”file:/./dev/random”都会起作用的原因。

在这个实现中，产生器会评估熵池（entropy pool）中的噪声数量。随机数是从熵池中进行创建的。当读操作时，/dev/random设备会只返回熵池中噪声的随机字节。/dev/random非常适合那些需要非常高质量随机性的场景，比如一次性的支付或生成密钥的场景。

当熵池为空时，来自/dev/random的读操作将被阻塞，直到熵池收集到足够的环境噪声数据。这么做的目的是成为一个密码安全的伪随机数发生器，熵池要有尽可能大的输出。对于生成高质量的加密密钥或者是需要长期保护的场景，一定要这么做。

那么什么是环境噪声？

随机数产生器会手机来自设备驱动器和其它源的环境噪声数据，并放入熵池中。产生器会评估熵池中的噪声数据的数量。当熵池为空时，这个噪声数据的收集是比较花时间的。这就意味着，Tomcat在生产环境中使用熵池时，会被阻塞较长的时间。

基本上就是这样，这里讲的更详细！

下面说解决方式：

网上说：

		通过修改Tomcat启动文件-Djava.security.egd=file:/dev/urandom
		
		通过修改JRE中的java.security文件securerandom.source=file:/dev/urandom

这两种方式在我这都失败，不起作用，不知道是我的问题，还是其他问题。

最终解决方式：

		yum install rng-tools安装rngd服务（熵服务）
		
		systemctl start rngd启动服务
		
		如果你的CPU不支持DRNG特性或者像我一样使用虚拟机，可以使用/dev/unrandom来模拟。
		
		cp /usr/lib/systemd/system/rngd.service /etc/systemd/system
		
		编辑/etc/systemd/system/rngd.service service小结，ExecStart=/sbin/rngd -f -r /dev/urandom
		
		systemctl daemon-reload重新载入服务

		systemctl restart rngd重启服务

这样安装了熵服务后问题就解决了，Tomcat启动又回到了以往的速度。
