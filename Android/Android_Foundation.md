# #安卓的基本框架

 

## ##内核层

```shell
支持多进程和多线程的Linux内核

每个应用程序都有自己的Linux ID，并在单独的进程中运行

具有相同ID的两个应用程序可以彼此交换数据
```



## ##系统运行层

```shell
主要是一些开源类库以及Android运行时环境

其中Dalvik虚拟机中运行的应用程序格式为dex的二进制文件
```



## ##应用框架层

```shell
具有Java接口的应用程序框架

主要组成

Android NDK

Android SDK
```



## ##应用层

```shell
预安装一些核心应用程序
```

# #APK打包编译流程



![image-20230726144547288](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144547288.png)

![image-20230726144640802](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144640802.png)

![image-20230726144647162](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144647162.png)

![image-20230726144653877](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144653877.png)

![image-20230726144702228](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144702228.png)

![image-20230726144707916](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726144707916.png)

## ##资源处理

```
使用aapt工具进行资源文件的处理

分析AndroidManifest.xml中的资源文件

生成R.java和resources.arsc文件

aidl工具负责处理aidl文件

生成对应的java接口文件
```



## ##代码编译

```
将上一过程中产生的R.java、java接口文件以及工程源代码一起通过Java Compiler编译成.class文件，打包成.jar文件

这一部分可以加入代码混淆

比如用ProGuard

然后与第三方库的Jar包一起通过dx文件转换成.dex文件

如果apk的方法超过65535，会生成多个dex文件

反编译的话需要对这多个dex文件均进行转换Jar包处理

通过apkbuilder工具将aapt生成的resources.arsc、classes.dex、其他的资源一块打包生成未签名的apk文件
```



## ##添加签名

```
通过Jarsigner对生成的未签名的apk进行签名

再通过zipalign对签名后的apk进行对齐处理。使apk中所有资源文件距离文件起始偏移为4字节的整数倍(因为dalvik是32位，ART64位兼容32位)，从而在通过内存映射访问apk文件时会更快，同时减少在设备上运行时的内存消耗
```

# #apk文件

```
apk = android application package**

apk文件是什么：安卓app的安装包

本质：apk文件其实就是个zip压缩包

可以用解压缩工具把apk当作zip一样去解压

解压后，得到一堆安卓相关文件

可以在apktool等工具破解和修改了安卓文件后，再重新用压缩文件工具或apktool等工具，重新打包为apk文件
```

 

## ##apk内容结构

```
AndroidManifest.xml
二进制xml文件，提供设备运行时应用程序所需的各种信息

classes.dex
以dex格式编译的应用程序代码

resources.arsc
包含预编译应用程序资源的二进制xml文件

res/
包含未编译到resources.arsc文件中的资源

assets/
包含应用程序的原始资产，由AssetManager提供对这些文件的访问

META-INF/
包含MANIFEST.MF文件，该文件存储有关JAR内容的元素。APK的签名也在该文件内

lib/
包含已编译的代码，例如本地代码库
```



# #dex文件

```
dex = Dalvik Executable format = dex文件 = dex格式

dex之于Android，类似于class之于Java

注：Java的class文件内部是Java的字节码(Java bytecode)

dex = Dalvik Executable

dex文件 = dex字节码

dex反汇编之后是smali代码
即Android(虚拟机中的dex文件)反汇编(后的)代码：smali
```

**参考**

```
dex格式
Dalvik可执行文件格式|Android开源项目|Android Open Source Project
https://source.android.com/devices/tech/dalvik/dex-format

字节码
Dalvik字节码|Android开源项目|Android Open Source Project
https://source.android.com/devices/tech/dalvik/dalvik-bytecode

安卓系统中，用Dalvik虚拟机(DVM = Dalvik Virtual Machine)将Java源代码编译为dex可执行文件(Dalvik Executable)

dex文件中保存的是:编译后的安卓程序代码文件
```

 

## ##dex文件内部格式

```
File Header

String Table

Class List

Field Table

Method Table

Class Definition Table

Field List

Method List

Code Header

Local Variable List
```

 

# #安卓虚拟机

```
Android 
代码语言：Java

Java虚拟机：JVM

Android出于性能考虑，没使用JVM
```

 

```
安卓虚拟机 = Android虚拟机 = Android VM

Android < 5.0用的Dalvik
  Dalvik VM = DVM 
    google专为Android设计的虚拟机

Android >= 5.0用的ART
  ART = Android RunTime
```

**参考** 

```
Android RunTime和Dalvik|Android开源项目

https://source.android.com/devices/tech/dalvik
```



## ##JVM vs DVM         

<img src="C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726150456938.png" alt="image-20230726150456938" style="zoom:150%;" />

**JVM**

```
基础：基于栈帧 stack-based

文件格式：java字节码 = java bytecode

效率：相对低
```

**DVM**

```
基础：基于寄存器 Register-based

文件格式：dex

效率：高于JVM 速度更快，占用空间更少
```



## ##ART

**ART = Android RunTime**

```
是安卓新一代的VM虚拟机，用以替代旧的Dalvik
```

**特点：**

```
预编译AOT

垃圾回收方面的优化

开发和调试方面的优化

支持采样分析器

支持更多调试功能

优化了异常和崩溃报告中的诊断详细信息
```

# #Smali

## ##Smali基础

```
是什么：一种汇编语法/汇编文件

一种语法：Smali语法

来源：dex文件中的二进制数据反汇编后得到Smali代码

语法：一种宽松式的Jasmin/dedexer语法

实现了dex格式所有功能(注释、调试信息、线路信息等)
```

**举例**

```
Java源码： int x= 42

dex：13 00 2A 00

smali: const/16 v0, 42
```

**用处**

```
分析APK：静态分析(不够)

需要动态分析(涉及smali)

修改APK逻辑：修改smali代码，重新编译打包APK

Android逆向基础
```

**官网**

```
https://github.com/JesusFreke/smali
```

**Smali/baksmali**

```
https://github.com/JesusFreke/smali
```

```
smali: assembler = 汇编器

smali语言 = 汇编语言

baksmali: disassembler = 反汇编器

安卓系统中Java虚拟机所使用的一种dex格式文件的反汇编器
```

## ##Smali语法

```
https://github.com/JesusFreke/smali/wiki/TypesMethodsAndFields
```

**数据类型**

| Smali          | Java     | 备注                                                         |
| -------------- | -------- | ------------------------------------------------------------ |
| V              | void     | 只能用于返回值类型                                           |
| Z              | boolean  |                                                              |
| B              | byte     |                                                              |
| S              | short    |                                                              |
| C              | char     |                                                              |
| I              | int      |                                                              |
| J              | long     |                                                              |
| F              | float    |                                                              |
| D              | double   |                                                              |
| Lpackage/name; | 对象类型 | L 表示这是一个对象类型  package/name 表示该对象所在的包  ; 表示对象名称的结束  Lpackage/name/ObjectName;  相当于java中的package.name.ObjectName; |
| [类型          | 数组     | [I 表示一个int型数组  [Ljava/lang/String表示一个String的对象数组 |

![image-20230726151201783](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726151201783.png)

![image-20230726151207661](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726151207661.png)

![image-20230726151215916](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726151215916.png)

**函数·类型**

```
direct method = private方法

virtual method = 其余的方法
```

**函数·包含**

```
invoke-direct

invoke-virtual

invoke-static

invoke-super

invoke-interface
```

**函数·保存返回结果**

```
move-result或move-result-object来保存函数返回的结果
```

# #寄存器

```
https://github.com/JesusFreke/smali/wiki/Registers
```

```
Java中变量都是存放在内存中的

Android为了提高性能，变量都存放在寄存器中

寄存器为32位，可以支持任何类型
```

**寄存器类型**

```
本地寄存器
  用v开头数字结尾的符号来表示
    v0,v1,v2

参数寄存器
  用p开头数字结尾的符号来表示
    p0,p1,p2
```

**注**

```
非static方法中，p0代指this，p1为方法中的第一个参数

static方法中，p0为方法中的第一个参数
```

**说明**

```
.registers 指定了方法中寄存器的总数

.locals 表明了方法中非参寄存器的总个数，出现在方法中的第一行
```

