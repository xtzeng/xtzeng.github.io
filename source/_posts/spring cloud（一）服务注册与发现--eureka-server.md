---
title: spring cloud（一）服务注册与发现--eureka-server
date: 2017-08-10 21:19:57
tags:
---

1、在默认设置下，Eureka服务注册中心也会将自己作为客户端来尝试注册它自己，所以我们需要禁用它的客户端注册行为。

禁止方式如下：


eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false

2.微服务架构

微服务架构是将一个完整的应用从数据存储垂直拆分成多个不同的服务，每个服务都能独立部署、独立维护、独立扩展，服务与服务之间通过诸如RESTful API的方式相互调用

3.服务注册与发现

如何使用Spring Cloud搭建服务注册与发现模块

我们会用到Spring Cloud Netflix,该项目是Spring Cloud的子项目之一，主要内容是对Netflix公司一系列开源产品的包装，它为Spring Boot应用提供了自配置的Netflix OSS整合。通过一些简单的注解，开发者就可以快速的在应用中配置一下常用模块并构建庞大的分布式系统。主要提供的模块包括：服务发现(Eureka),断路器(Hystrix),智能路由(Zuul),客户端负载均衡(Ribbon)等。

4.创建“服务注册中心”

创建一个基本的Spring Boot工程，并在pom.xml中引入如下内容：

```xml
 
	 <parent>
	  		<groupId>org.springframework.boot</groupId>
	  		<artifactId>spring-boot-starter-parent</artifactId>
	  		<version>1.3.7.RELEASE</version>
	  		<relativePath></relativePath>
	  </parent>

	<dependency>
	    <groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
    </dependency>
    
     <dependency>
        <groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-eureka-server</artifactId>
    </dependency>

 	<dependencies>
        <dependency>
		    <groupId>org.springframework.cloud</groupId>
		    <artifactId>spring-cloud-dependencies</artifactId>
		    <version>Brixton.RELEASE</version>
		    <type>pom</type>
		    <scope>import</scope>
		</dependency>
    </dependencies>，

```

5.通过@EnableEurekaServer注解启动一个服务注册中心提供给其他应用进行对话。这一步非常简单，只需要在一个普通的Spring Boot项目中添加这个注解就能开启此功能，如下：

```java

	@EnableEurekaServer
	@SpringBootApplication
	public class MiaoMiaoApplicationEurekaServer {
		public static void main(String[] args) {
			new SpringApplicationBuilder(MiaoMiaoApplicationEurekaServer.class).web(true).run(args);
		}
	}
```

6.在默认的设置下，该服务注册中心也会将自己作为客户端来尝试注册它自己，所以我们需要禁用它的客户端注册行为，只需要在application.properties中增加如下配置：

```javascript

	server.port=1111
	eureka.client.register-with-eureka=false
	eureka.client.fetch-registry=false
	eureka.client.serviceUrl.defaultZone=http://${eureka.instance.hostname}:${server.port}/eureka/
```

7.为了和后续要进行注册的服务区别，这里将服务注册中心的端口通过server.port属性设置为1111.

启动工程后，访问：[http://localhost:1111/](http://localhost:1111/)

8.创建“服务提供方”

下面我们创建提供服务的客户端，并向服务注册中心注册自己。

首先，我们再创建一个Spring Boot 应用，并在pom.xml中加入以下配置：

```xml

		<dependency>
    		<groupId>org.springframework.boot</groupId>
    		<artifactId>spring-boot-starter-test</artifactId>
    		<scope>test</scope>
    	</dependency>
		<dependency>
    		<groupId>org.springframework.cloud</groupId>
    		<artifactId>spring-cloud-starter-eureka</artifactId>
    	</dependency>
```

其次，我们实行/hello请求处理接口，通过DiscoveryClient对象，在日志中打印出服务实例的相关内容。

```java

	@RestController
	public class HelloWorldController {
	
	private final Logger logger = Logger.getLogger(getClass());
	
	@Autowired
	private DiscoveryClient discoveryClient;
	
	
	@RequestMapping(value = "/hello",method = RequestMethod.GET)
	public String hello() throws Exception{
		
		ServiceInstance instance = discoveryClient.getLocalServiceInstance();
		
		//测试超时触发断路器
		int sleepTime = new Random().nextInt(3000);
		logger.info("sleepTime:--------->>>>"+sleepTime);
		Thread.sleep(sleepTime);
		
		logger.info("/hello,host:--->>>"+instance.getHost()+",service_id:--->>>"+instance.getServiceId());
		
		return "Hello World";
	}

}
```

最后在主类中通过加上@EnableDicoveryClient注解，该注解能激活Eureka中的DicoveryClient实现，才能实现Controller中对服务信息的输出。

```java


	@EnableDiscoveryClient
	@SpringBootApplication
	public class MiaoMiaoServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(MiaoMiaoServiceApplication.class,args);
	}
}

```

在完成了服务内容的实现之后，再继续对application.properties做一些配置工作，具体如下：



```javascript


	spring.application.name=miaomiao-spring-cloud-eureka-service
	server.port=8082
	eureka.client.serviceUrl.defaultZone=http://localhost:1111/eureka/

```

通过spring.application.name属性，我们可以指定微服务的名称后续在调用的时候只需要使用该名称就可以进行服务的访问。

eureka.client.serviceUrl.defaultZone属性对应服务注册中心的配置内容，指定服务注册中心的位置。

为了在本机上测试区分服务提供方跟服务注册中心，使用server.port属性设置不同的端口。

启动该工程后，再次访问：http://localhost:1111/

可以看到，我们定义的服务被注册了。





