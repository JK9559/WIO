### 服务器性能剖析
---
#### 性能优化简介
1. 性能的定义是什么？性能就是完成某件任务所需要的时间度量。

#### 对应用程序进行性能剖析
1. 使用工具对应用程序进行监控，主要的性能问题体现在：
    + 调用了外部资源
    + 需要处理大量问题或者数据
    + 循环中执行耗时的操作
    + 算法不优化

#### 剖析 ```MySQL``` 查询
1. 通过慢查询日志，但是当慢查询日志的权限不足的时候，有两种替代技术，都集成在 ```pt-query-digest```：
    + 通过 ```--processlist``` 不断查看 ```SHOW FULL PROCESSLIST``` 记录查询第一次出现的时间和消失的时间。缺点是无法精确获得较短时间的查询。
    + 通过抓取 ```TCP``` 网络包，然后根据 ```MySQL``` 的客户端/服务端通信协议进行解析。可以先通过 ```tcpdump``` 将网络包数据存到磁盘，然后用 ```pt-query-digest``` 的 ```--type=tcpdump``` 来解析分析。精度较高。
2. 分析慢查询日志：
    + 本书中使用了 ```pt-query-digest``` 工具分析了慢查询日志，分为几列，含义为 ```Query ID``` 对查询语句计算的哈希值。 ```Response time``` 该语句总执行时间。 ```Calls``` 语句总调用次数。 ```R/Call``` 单次查询执行时间。 ```V/M``` 方差均值比，越大说明查询时间波动越大，需要优化。
3. 通过上面的分析，找到了需要优化的语句，可以针对单条查询进行剖析，有三种方式
    + ```SHOW PROFILE```：
        + 执行 ```SQL```
        + 执行 ```SHOW PROFILES``` 查询得到要查询的 ```SQL``` 的 ```Query_ID```
        + 执行 ```SHOW PROFILE FOR QUERY <Query_ID>```
        + 缺点就是 没法格式化
    + ```SHOW STATUS```：
        + 记录了一个全局的计数器，可以在查询结束后，观察某些计数器的值。
        + ```FLUSH STATUS``` ：会话级别计数器置为 0
        + 执行查询语句
        + ```SHOW STATUS WHERE Variable_name LIKE 'Handler%' OR Variable_name LIKE 'Created%';```
            + 初步解析 参数 ```Created_tmp_tables``` 使用了多少临时表 ```Created_tmp_disk_tables``` 几个磁盘临时表 注意 ```SHOW STATUS``` 本身的查询也会被统计进入报告。
    + 使用慢查询日志
        + 使用 ```pt-query-digest``` 工具
4. 