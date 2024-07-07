<!--
 * @Name: 
 * @Copyright: 
 * @Author: 
 * @Date: 18/06/24 19:23
 * @Description: 
-->
# Stamon2-portable

此项目为[Stamon2](https://github.com/CLimber-Rong/stamon2)的便携版。

此版本删除了编译器部分，只保留了虚拟机，用于更轻量的平台对stamon进行移植。

**目前便携版改编于2.4.6发行版**

### 编译方法

**注意：接下来的步骤假定编译平台支持C语言标准库，如若不支持，请看下一部分“移植方法”**

输入如下指令：

```Makefile
$(COMPILER) src/Main.cpp -o bin/stamon.exe -O2 -std=c++17 -I include/stdc_implemented -I src/ast -I src/data_type -I src/vm -I src/ir -I src/compiler -I src/sfn -I src -lm
```

将``$(COMPILER)``替换成其他C++编译器即可（例如g++）

如果有条件，可以再执行以下命令将程序压缩：

```
strip -s bin/stamon.exe
upx -9 bin/stamon.exe
```

### 移植方法

先将``include/template``里提供的接口实现，然后输入以下指令进行编译。

```Makefile
$(COMPILER) src/Main.cpp -o bin/stamon.exe -O2 -std=c++17 -I include/template -I src/ast -I src/data_type -I src/vm -I src/ir -I src/compiler -I src/sfn -I src -lm
```

将``$(COMPILER)``替换成其他C++编译器即可（例如g++）

### 使用方法

``stamon source [options...]``

其中source为生成的字节码路径，[options...]为可选的运行选项，分别为：

* --isGC=&lt;boolean&gt;：是否支持GC，默认为true
* --MemLimit=&lt;Integer&gt;：对象内存大小上限，默认为16MiB