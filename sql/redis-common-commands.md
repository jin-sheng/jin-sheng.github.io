# Redis 常用命令

监控每秒操作数
```shell
# ./redis-cli info | grep ops
```

查看被阻塞的客户端
```shell
# ./redis-cli info | grep blocked_clients
```

查看由于最大内存限制被移除的 key 的数量
```shell
# ./redis-cli info | grep evicted_keys
```

查看内存碎片率
```shell
# ./redis-cli info | grep mem_fragmentation_ratio
```

查看已使用内存
```shell
# ./redis-cli info | grep used_memory:
```

查看连接情况
```shell
# ./redis-cli info | grep connected
```

查看 key 值命中情况
```shell
# ./redis-cli info | grep keyspace
```

查看缓冲区大小
```shell
# ./redis-cli info | grep backlog_size
```

测试 100 个连接、5000 次请求对应的性能
```shell
# ./redis-benchmark -c 100 -n 5000
```

## 参考
[Redis性能指标监控](https://blog.51cto.com/yht1990/2503819)  
