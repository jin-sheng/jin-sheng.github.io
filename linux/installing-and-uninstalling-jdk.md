# Linux 安装与卸载 JDK

## RPM 方式

安装 JDK
```shell
# chmod 755 jdk-8u102-linux-x64.rpm
# rpm -i jdk-8u102-linux-x64.rpm
```

查看 RPM 方式安装的 JDK 列表
```shell
# rpm -qa | grep jdk
```

查看 java 指令的位置
```shell
# whereis java
```

卸载 RPM 方式安装的 JDK
```shell
# rpm -e --nodeps jdk1.8.0_102-1.8.0_102-fcs.x86_64
```
