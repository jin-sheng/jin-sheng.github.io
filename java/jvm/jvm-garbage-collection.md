# JVM 垃圾回收
常见的回收算法

|模式|区域|算法名称|说明|
|---|---|---|---|
|串行 GC|||GC时由单个线程来完成，适合 CPU 数量少、内存小的应用|
||Old|Tenured||
|Parallel GC||||
||Young|PSYoungGen||
||Old|PSOldGen||
||Perm|PSPermGen||
|Parallel Old GC||||
||Old|ParOldGen||
|CMC GC|||适合管理更大的内存|
||Young|ParNew||
|G1||||
