### 1、vs调试
- 逐语句 step into  进入方法
- 逐过程 step over 遇到方法跳过
- 跳出    step out

### 2、发生异常的时候要查看InnerException查看之前的异常，一路挖深，找到为值为null的才是最早的异常。


### 3、使用finally确保关键代码总是运行（比如释放文件的）