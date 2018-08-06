# Signal
一个高性能的事件系统（信号系统）

### 使用场景
可以完全替换C#原生的Action，以及UnityEvent。  

### 主要优势
其综合性能完胜C#的原生Action以及UnityEvent。  
由于是自己实现的封装，可以在代码中插入日志，对信号的流向进行动态追踪。  
以及用TryCatch对异常进行隔离（不会因为其中一个监听者出现异常造成其它监听者无法收到信号）。  

### 性能对比
将Signal对比SystemAction和UnityEvent，进行10万次调用，结果如下(IPhone6)：  
![image](https://github.com/slicol/Signal/blob/master/images/performance.png)  
红色的是Signal，蓝色的是UnityEvent，棕色的是SystemAction

当监听者数量少于30个时，调用耗时：SystemAction < Signal <<< UnityEvent  
当监听者数量大于30个时，调用耗时：Signal << SystemAction << UnityEvent  

### 内存对比
对Signal、SystemAction和UnityEvent，分别Add/Remove1000次，结果如下：  
在Add时：Signal预设Capacity(0kb) < Signal(16.3kb) < UnityEvent(39.8kb) <<< SystemAction(49.6mb)  
在Remove时：Signal(0kb) <<< UnityEvent(203.3kb) <<< SystemAction(49.5mb)  

### 综合结论
Signal在综合性能方面几乎完胜原生Action和UnityEvent。  
并且如果在一些需要频繁Add和Remove监听者的场景下，Signal更加是最优的。
