# 阿里云 API Java封装库 使用指南

## 背景介绍
Fit2Cloud是一个建立在IaaS之上的DevOps协作平台，帮助开发人员、测试人员以及运维人员实现应用全生命周期的
自动化管理，包括创建环境、软件安装、代码部署、自动配置、监控告警和自动伸缩等。Fit2Cloud打通了从代码到服务的
转化通道，实现了云应用的持续交付和自动化运维，极大地提高了开发和运维的效率。

在亚马逊(AWS)云生态圈中，AWS及其合作伙伴提供了多种应用部署和管理工具，比如CloudFormation、Opsworks、
Beanstalk、Rightscale、Scalr等，但是在阿里云生态圈中目前没有这样的工具，可以说Fit2Cloud填补了这个空白。

我们在开发[**FIT2CLOUD for 阿里云**](http://aliyun.fit2cloud.com/)过程中，需要调用ECS API进行各种操作。 
我们的后端采用的是Java语言，所以我们使用java语言完整封装了ECS的API。
我们相信云计算的使用哲学是通过API(或者基于API的第三方工具)来动态管理资源，
因此我们决定将我们封装好的ECS API Java SDK开源出去。

## 第一步：引用Jar包

### 方法1：使用Maven

```xml

<!-- repository -->
<repositories>
	<repository>
		<id>fit2cloud</id>
		<url>http://repository.fit2cloud.com/content/groups/public/</url>
		<releases>
			<enabled>true</enabled>
		</releases>
		<snapshots>
			<enabled>true</enabled>
		</snapshots>
	</repository>  
</repositories>

<!-- dependency -->
<dependency>
  <groupId>com.fit2cloud</groupId>
  <artifactId>aliyun-api-java-wrapper</artifactId>
  <version>1.1</version>
</dependency>
```

### 方法2：直接下载Jar包

下载地址是：
http://repository.fit2cloud.com/service/local/repo_groups/public/content/com/fit2cloud/aliyun-api-java-wrapper/1.1/aliyun-api-java-wrapper-1.1-jar-with-dependencies.jar

## 第二步：调用Aliyun ECS API

```java
 		String ACCESS_KEY_ID = "你的阿里云API Access key";
    	String ACCESS_KEY_SECRET = "你的阿里云API Secret key";
        ECSClient client = new ECSClient(new AliyunCredentials(ACCESS_KEY_ID, ACCESS_KEY_SECRET));
        ListRegionsResponse response = client.listRegions();		
```
目前仅封装了ECS相关API，包括

1. allocatePublicIp: 为虚机分配公有IP
2. attachDisk: 为虚机添加独立云磁盘
3. authorizeSecurityGroup: 为安全组添加规则
4. createDisk: 创建独立云磁盘
5. createImage: 创建镜像
6. createInstance: 创建虚机
7. createSecurityGroup: 创建安全组
8. createSnapshot: 创建快照
9. deleteDisk: 删除独立云磁盘
10. deleteImage: 删除镜像
11. deleteInstance: 删除虚机
12. deleteSecurityGroup: 删除安全组
13. deleteSnapshot: 删除快照
14. detachDisk: 从虚机移除独立云磁盘
15. getInstance: 获取虚机信息
16. joinSecurityGroup: 将虚机加入安全组
17. leaveSecurityGroup: 将虚机移除出安全组
18. listAutoSnapshotPolicy: 获取自动快照策略
19. listDisks: 获取磁盘列表
20. listImages: 获取镜像列表
21. listInstanceMonitorData: 获取指定监控数据
22. listInstances: 获取虚机列表
23. listInstanceType: 获取虚机类型列表
24. listRegions: 获取数据中心列表
25. listSecurityGroups: 获取安全组列表
26. listSecurityPermissions: 获取安全组规则列表
27. listSnapshots: 获取快照列表
28. listZones: 获取可用区列表
29. modifyAutoSnapshotPolicy: 修改自动快照策略
30. modifyDiskAttribute: 修改独立云磁盘参数
31. modifyInstanceAttribute: 修改虚机参数
32. rebootInstance: 重启虚机
33. reInitDisk: 重新初始化磁盘
34. replaceSystemDisk: 替换系统盘
35. resetDisk: 使用指定磁盘自身的快照回滚磁盘内容
36. revokeSecurityGroup: 取消安全组规则
37. startInstance: 启动虚机
38. stopInstance: 暂停虚机

每个API调用都会有两类异常：

1. AliyunClientException: 客戶端錯誤，比如网络问题
2. AliyunServiceException: 服务器端错误，阿里云会返回错误代码和具体消息

目前支持的ECS API版本为: API 版本 2014-05-26
