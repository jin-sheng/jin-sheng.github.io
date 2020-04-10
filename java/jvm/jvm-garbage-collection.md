# JVM 垃圾回收
常见的回收算法

|区域|模式|算法名称|说明|
|---|---|---|---|
|Old|串行 GC|Tenured|GC时由单个线程来完成|
|Young|Parallel GC|PSYoungGen||
|Old|Parallel GC|PSOldGen||
|Perm|Parallel GC|PSPermGen||
|Old|Parallel Old GC|ParOldGen||
|Young|CMC GC|ParNew|适合管理更大的内存|
||G1|||
