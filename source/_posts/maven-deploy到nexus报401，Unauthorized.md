---
title: maven deploy到nexus报401，Unauthorized
date: 2017-10-09 17:18:55
tags: [maven,nexus]
---

提交到nexus时候报错：


[ERROR] Failed to execute goal org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy (default-deploy) on project *: Failed to deploy artifacts: Could not transfer artifact *:jar:1.0 from/to releases (http://10.1.81.199:8081/nexus/content/repositories/releases/): Failed to transfer file: http://10.1.81.199:8081/nexus/content/repositories/releases/com/cs2c/security-management-client* /1.0/*-1.0.jar. Return code is: 401, ReasonPhrase:Unauthorized.

原来是没有配置认证。

maven目录conf的setting.xml里，

	<servers>
  		<server>  
    		<id>releases</id>  
    		<username>admin</username>  
    		<password>admin123</password>  
  		</server>  
 		<server>  
  			<id>snapshots</id>  
  			<username>admin</username>  
  			<password>admin123</password>  
  		</server>  
	</servers>

用户名和密码都是nexus的。再次deploy即可。

注意这里的id要和pom.xml里远程deploy的地址对应一致，我的pom.xml里配置：

<!-- 配置远程发布到私服，mvn deploy -->  
    <distributionManagement>  
        <repository>  
            <id>releases</id>  
            <name>Nexus Release Repository</name>  
            <url>http://10.1.81.199:8081/nexus/content/repositories/releases/</url>  
        </repository>  
        <snapshotRepository>  
            <id>snapshots</id>  
            <name>Nexus Snapshot Repository</name>  
            <url>http://10.1.81.199:8081/nexus/content/repositories/snapshots/</url>  
        </snapshotRepository>  
    </distributionManagement>

如果这里不配置，会报错：

报错：Failed to execute goal org.apache.maven.plugins:maven-deploy-plugin:2.5:deploy (default-deploy) on project git-demo: Deployment failed: repository element was not specified in the POM inside distributionManagement element or in -DaltDeploymentRepository=id::layout::url parameter
