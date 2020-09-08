# 安装 ```ClickHouse```

1. ```sudo yum install yum-utils```
2. ```sudo rpm --import https://repo.clickhouse.tech/CLICKHOUSE-KEY.GPG```
3. ```sudo yum-config-manager --add-repo https://repo.clickhouse.tech/rpm/clickhouse.repo```
4. ```sudo yum install clickhouse-server clickhouse-client```

5. ```sudo /etc/init.d/clickhouse-server start```
6. ```clickhouse-client```

> 遇到的问题：
> ```Code: 210. DB::NetException: Connection refused (localhost:9000)```
>
> 解决方案：
> 
> ```service clickhouse-server start```
>
> ```clickhouse-client```