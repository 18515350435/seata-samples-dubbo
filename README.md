#启动步骤
##业务数据库mysql中建立业务表
执行文件 业务数据库表.sql 中的sql
理论上应该建立在seata-samples-dubbo\dubbo\src\main\resources\jdbc.properties配置文件中三个不同的数据库中，
例子中为了省事放到了一个数据库，自己可以修改建立seata1、seata2、seata3存放三个业务表undo_log表要在三个业务数据库都有，

##事务协调器seataserver存储协调事务的相关表结构
因为例子中seataserver选择的存储模式是db类型，所以有以下建表操作
执行文件 db_store模式需要的表.sql 中的sql
理论上应该建立在eata-samples-master\seata-samples-dubbo\AAseata-server\conf\file.conf配置文件中db配置下的数据库中

##zookeeper
本示例中为了方便使用将dubbo的实例serviceBean注册和管理事务协调器seataserver的集群使用的都是同一个zookeeper管理的，
真实中应使用不同的，

##启动过程
启动seata-samples-master\seata-samples-dubbo\AA-apache-zookeeper-3.5.8-bin\bin\zkServer.cmd
为了演示集群启动三个seata-server在三个不同的端口上
启动seata-samples-master\seata-samples-dubbo\AAseata-server\bin\seata-server.bat -p 8091
启动seata-samples-master\seata-samples-dubbo\AAseata-server\bin\seata-server.bat -p 8092
启动seata-samples-master\seata-samples-dubbo\AAseata-server\bin\seata-server.bat -p 8093

启动DubboAccountServiceStarter
启动DubboOrderServiceStarter
启动DubboStorageServiceStarter
启动调试程序【建议Debug模式启动加断点】DubboBusinessTester：在抛异常地方打断点观察数据库中数据，加深理解

