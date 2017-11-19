---
title: How to set the max size of upload file
date: 2017-11-19 16:06:19
tags: [spring]
---

I'm developing application based on Spring Boot and AngularJS using JHipster. My question is how to set max size of uploading files?

If I'm trying to upload to big file I'm getting this information in console

	 DEBUG 11768 --- [io-8080-exec-10] c.a.app.aop.logging.LoggingAspect: 
	
	Enter: com.anuglarspring.app.web.rest.errors.ExceptionTranslator.processRuntimeException() with argument[s] = 
	
	[org.springframework.web.multipart.MultipartException: Could not parse multipart servlet request; nested exception is java.lang.IllegalStateException: 
	
	org.apache.tomcat.util.http.fileupload.FileUploadBase$FileSizeLimitExceededException: The field file exceeds its maximum permitted size of 1048576 bytes.]

Also in Spring boot 1.4, you can add following lines to your application.properties to set the file size limit:

	spring.http.multipart.max-file-size=128KB
	spring.http.multipart.max-request-size=128KB



There is some difference when we define the properties in the application.properties and application yaml.

In application.yml :
	
	spring:
    	http:
      	  multipart:
       	     max-file-size: 256KB
      	     max-request-size: 256KB

And in application.propeties :
		
		spring.http.multipart.max-file-size=128KB
		spring.http.multipart.max-request-size=128KB

