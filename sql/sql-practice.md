# SQL 实践

## 不能使用索引的情况

负向条件查询
```sql
select * from order where status != ...
select * from order where status not in ...
select * from order where not exists ...
-- 可优化为 in 查询
select * from order where status in ...
```

前导模糊查询
```sql
select * from order where desc like '%...'
-- 可优化为非前导模糊查询
select * from order where desc like '...%'
```


# 参考
[或许你不知道的12条SQL技巧](https://mp.weixin.qq.com/s/AwAEJVWtYfiy79jXGC7olA)  
