# springbootRedisSlaverSentine
windows下redis实现一主二从三哨兵，springboot项目配置哨兵信息，操作redis

1:windows版redis下载地址 https://github.com/MicrosoftArchive/redis/tags

本例使用的
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/win-3.2.100.png)

2:将下载好的redis压缩文件解压到redisMaster中，我删掉了其中一个conf文件，将redisMaster目录下的redis.windows.conf文件作为主服务的配置文件。并修改了dbfilename/logfile相关配置，其余保持默认不变。
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/redisMaster.png)

3:创建redisSlaverOne文件夹并复制一份redis.windows.conf配置文件。修改了dbfilename/logfile相关配置，注* 修改配置文件中的端口号为6380,并添加从服务配置：slaveof 127.0.0.1 6379
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/redisSlaverOne.png)

4:创建redisSlaverTwo文件夹并复制一份redis.windows.conf配置文件。修改了dbfilename/logfile相关配置，注* 修改配置文件中的端口号为6381,并添加从服务配置：slaveof 127.0.0.1 6379
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/redisSlaverTwo.png)

5:以上配置便完成了基本的一主二从的相关配置，当启动完三个服务后可通过命令info replication检查知否有slaves服务实例
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/slavesList.png)

6:分布创建sentinelOne，sentinelTwo，sentinelThree哨兵文件夹并分别设置sentinel配置文件。

7创建springboot项目并在yml配置文件中增加redis哨兵
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/yml.png)

8:重写redisConnectionFactory  redisTemplate
![](https://raw.githubusercontent.com/WTG2010/springbootRedisSlaverSentine/master/img/sentinelConfig.png)

9:使用测试


