# Linux Crontab 定时任务

编辑脚本
```shell
# vi /path/custom.sh
```

设置只有拥有者有读、写、执行权限
```shell
# chmod 700 /path/custom.sh
```

测试脚本
```shell
# /path/custom.sh
```

设置定时任务
```shell
# vi /etc/crontab
```

```shell
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
```

查看 crontab 日志
```shell
# less /var/log/cron
```

参考
[Linux Crontab 定时任务](https://www.runoob.com/w3cnote/linux-crontab-tasks.html)
