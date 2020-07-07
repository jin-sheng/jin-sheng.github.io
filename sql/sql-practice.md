# SQL 实践

## 不能使用索引的情况

负向条件查询
```sql
SELECT * FROM order WHERE status != ...
SELECT * FROM order WHERE status not in ...
SELECT * FROM order WHERE NOT EXISTS ...
-- 可优化为 in 查询
SELECT * FROM order WHERE status IN ...
```

前导模糊查询
```sql
SELECT * FROM order WHERE desc LIKE '%...'
-- 可优化为非前导模糊查询
SELECT * FROM order WHERE desc LIKE '...%'
```

不满足复合索引最左前缀
```sql
-- 现有复合索引(username,password)
-- 不能够命中索引
SELECT * FROM user WHERE password = ...
-- 能够命中索引
SELECT * FROM user WHERE username = ... AND password = ...
SELECT * FROM user WHERE password = ... AND username = ...
SELECT * FROM user WHERE username = ...
```

## 提高效率

是否存在
```sql
SELECT 1 FROM user WHERE username = ... AND password = ... LIMIT 1
```

查询结果只有一条时，明确告诉数据库，让它主动停止游标移动
```sql
SELECT * FROM user WHERE username = ... AND password = ... LIMIT 1
```

只返回需要的列，节省数据传输量与数据库的内存使用量
```sql
SELECT username,password FROM user
```

# 参考
[或许你不知道的12条SQL技巧](https://mp.weixin.qq.com/s/AwAEJVWtYfiy79jXGC7olA)  
