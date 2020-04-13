# Java 常用工具

查看 Java 版本
```shell
# java -version
```

查看字节码
```shell
# javap -verbose <类名称>
```

过滤出 Java 本身的进程以及运行的引导类
```shell
# jps -l
```

查看 JVM 中每个区域的情况（每 1000ms 采集一次数据，共采集两次数据）
```shell
# jstat -gcutil <pid> 1000 2
```

输出线程信息
```shell
# jstack -l <pid>
```

查看内存使用情况的基本信息
```shell
# jmap -heap <pid>
```
