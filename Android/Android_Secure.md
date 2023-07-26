# #加密加固的原因

安卓应用使用java或者kotlin开发，此处讨论java，主要是kotlin没看

```
极易被破解

导致代码或关键接口暴露
甚至被别人加入广告、病毒等二次打包发布
给公司或用户带来风险
```

**加固的缺点**

```
应用体积变大

启动速度变慢

无法在某些平台正常运行

有些加固方案需要收费

部分市场拒绝加壳后的应用上架
```

# #加密技术的历史

## ##原始社会时期

```
主要方式：代码混淆
```

## ##奴隶社会时期

```
主要方式：自我校验
```

## ##封建社会时期

```
主要方式：dex文件变形
```

## ##资本主义时期

### ###dex保护

**隐藏dex文件**

```
把dex隐藏,再通过另外的方式加载

通过加密甚至压缩将dex转换成另一个文件，而加固后的apk里面的dex则是用以加载dex的入口，也就是壳。

小花生v3.6.9和康美通v4.4.0？
```

**对dex文件进行变形**

```
让dex保留在外面，但dex里的内容是不完整的
```

**对dex结构进行变形**

```
dex结构中包含DexClassDef、ClassDataltem、DexCode。且DexCode中包含虚拟机运行的字节码指令

抽取dex结构中的文件，对字节码指令添加nop并做修复修正(修复修正是因为dex的校验)，即使校验通过也还有一些偏移问题

一般在运行前做修正，以减少工作量，有时候需要借助hook
```



### ###so保护

**修改Elf头、节表**

```
相关工具：010Editor  IDA
```

**选择开源加壳工具**

```
相关壳：UPX壳  支持arm架构的ELF加固
```

**进程防调试或增加调试难度**

```
调试一个进程首先要ptrace这个进程

故需要防止进程被ptrace
```

## ##社会主义时期

### ###之前遗留的问题

**隐藏dex遗留的问题**

```
破解办法
  实现自定义rom
  利用Inject原理将目标进程注入，代码进行hook系统函数来达到脱壳的目的

FDex2和DumpDex感觉就这样的？
```

**dex结构变形带来的弊端**

```
安卓5.0新增ART
  ART可以直接将dex编译为本地指令运行

dex结构变形遗留的问题很显然
  兼容性
  ART模式下的编译问题
```

**ELF简单修改遗留问题**

 

**UPX方面的劣势**

```
虽然UPX是so加壳的首选，但是upx代码逻辑复杂，难定制，难同时支持多种架构

故第三方加固产品仅简单使用upx加壳，并修改一些数据。不过容易被破解
```



### ###新防护技术

```
llvm混淆(据说破解后也难看懂代码)

VMP
```

# #加密方案概述

**代码混淆**

```
常用(Android自带的)ProGuard
```

**第三代加固技术**

```
对源apk整体加固，放到指定位置，运行的时候再解密动态加载
  对apk加固的破解，即脱壳
    Dex Method代码动态解密

对so进行加固，在so加载内存的时候进行解密释放
  对so的加固的破解，即so库反编译
    So代码膨胀混淆
```

**破解方案：基于hook框架，从安卓app中导出dex文件**

```
典型的hook框架

XPosed：从根上hook了Android Java虚拟机

Cydia：支持jni和java层的hook功能

再从dex中转换出java代码
```

**厂商意识到，只是代码用java写，运行在java层，那么被破解篡改的概率很大**

```
故将很多重要代码放在JIN层
  比如：微信的数据库连接操作

不过从破解的技术角度而言
  加壳，则脱壳
  so，则IDA调试
  反调试(检测)，则绕过去

```

# #防护安卓的安全

## ##加强业务逻辑

```
api接口通信

全部接口实现https

证书绑定SSL Pinning
```



## ##加强安全防破解技术

**代码**

```
代码混淆

Obfuscator-LLVM

ProGuard
```

**其他防护**

```
VMP

给dex(中的核心逻辑)做VMP
给so库(中的核心逻辑)做VMP
```

```
加壳

第三方加壳服务或自己实现
第三方加壳服务商
腾讯乐固legu
360加固保
网易易盾
```

# #代码混淆

**含义**

```
把原先的代码通过变量替换方式，使代码不可读，很难读
```

**目的**

```
增加破解人员读懂原先代码逻辑的难度 
```

**技术方案**

```
ProGuard

Obfuscator-LLVM
```

## ##ProGuard

**作用**

```
压缩 = Shrinking
移除未被使用的类、属性、方法等，并在优化动作执行后再次执行
(因为优化后可能会再次暴露一些未被使用的类和成员)

优化 = Optimization
优化字节码，并删除未使用的结构

混淆 = Obfuscation
将类名、属性名、方法名混淆为难以读懂的字母，增大反编译难度
```

**输出文件说明**

```
dump.txt：说明APK中所有类文件的内部结构

mapping.txt：提供原始与混淆过的类、方法、字段名称之间的转换和对应关系

seeds.txt：列出未进行混淆的类和成员

usage.txt：列出从APK移除的代码
```

**注**

**有些库，混淆后，导致代码不可用，故出现库，专门支持了ProGuard**

```
okhttp

https://github.com/square/okhttp

If you are using R8 or ProGuard add the options from okhttp3.pro

https://square.github.io/okhttp/r8_proguard/
```

**有些库，需要额外处理**

```
PermissionGen

https://github.com/lovedise/PermissionGen

打包混淆以后就废了，需要自己加配置，避免部分模块被混淆，才勉强可用

https://blog.csdn.net/dobiman/article/details/78595709\
```



## ##Obfuscator-LLVM

**功能特性**

```
指令替换
-mllvm -sub
https://github.com/obfuscator-llvm/obfuscator/wiki/Instructions-Substitution

Bogus控制流
-mllvm -bcf
https://github.com/obfuscator-llvm/obfuscator/wiki/Bogus-Control-Flow

控制流扁平化 = 控制流平坦化
-mllvm -fla
https://github.com/obfuscator-llvm/obfuscator/wiki/Bogus-Control-Flow

函数注解
https://github.com/obfuscator-llvm/obfuscator/wiki/Bogus-Control-Flow
```

**应用**

```
加固厂商使用改进的Obfuscator-LLVM对so文件中一些关键函数采用Obfuscator-LLVM混淆，增加逆向难度

用Obfuscator-LLVM混淆native代码，膨胀so
```

**文档**

```
Github obfuscator-llvm/obfuscator
https://github.com/obfuscator-llvm/obfuscator

obfuscator-llvm/obfuscator Wiki
https://github.com/obfuscator-llvm/obfuscator/wiki

obfuscator-llvm/obfuscator at llvm-4.0
https://github.com/obfuscator-llvm/obfuscator/tree/llvm-4.0
```

​                               

# #LLVM

llvm = Low Level Virtual Machine

![image-20230726160442637](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726160442637.png)

**LLVM**

```
http://www.llvm.org/
```

**Clang**

```
http://clang.llvm.org/
```

**LLDB**

```
http://lldb.llvm.org/
```

**libc++**

```
http://libcxx.llvm.org/
```

**libc++ ABI**

```
http://libcxxabi.llvm.org/
```

**compiler-rt**

```
http://compiler-rt.llvm.org/
```

**MLIR**

```
http://mlir.llvm.org/
```

**OpenMP**

```
http://openmp.llvm.org/
```

**polly**

```
http://polly.llvm.org/
```

**libclc**

```
http://libclc.llvm.org/
```

**klee**

```
http://klee.llvm.org/
```

**LLD**

```
http://lld.llvm.org/
```

# #花指令

**名称**

```
花指令又称为垃圾指令

指令其实就是字节 JunkBytes

加花，就是把花指令加到代码中
```

**起源**

```
花指令一词源于汇编语言
```

**含义**

```
在真实的代码中插入一些无用的、垃圾的代码/指令/字节，但又不会改变程序的原始逻辑，原有程序可正确执行
```

**目的**

```
反汇编工具在反汇编时会出错，导致反编译工具失效，提高破解难度

隐藏掉不想被逆向工程的代码块，使其没那么容易反编译

即使反编译后也难理解，增加破解和逆向的难度
```

**主要思想**

```
当花指令与正常指令的开始几个字节被反编译工具识别成一条指令的时候，则会导致反编译工具报错

插入的花指令都是一些随机的但是不完整的指令
```

**前提条件**

```
程序运行时，花指令位于一个永远也不会被执行的路径中

花指令是合法指令的一部分，只不过不完整而已
```

**实现思路**

```
在每个要保护的代码块之前插入无条件分支语句和花指令
```

**反汇编工具常用算法**

[]线性扫描算法

```
逻辑：依次按顺序逐个将每一条指令反汇编成汇编指令

结果：容易把花指令错误识别，导致反汇编出错
```

[]递归扫描算法

```
逻辑：按顺序逐个反汇编指令

如果某个地方出现了分支，就会把这个分支地址记录下来，让后对这些反汇编过程中遇见的分支进行反汇编

结果：反汇编能力更强
```

**常见Android逆向工具中的反汇编算法**

| 线性扫描算法 | DexDump  | jeb        | Ded     |        |
| ------------ | -------- | ---------- | ------- | ------ |
| 递归扫描算法 | baksmali | Androguard | IDA Pro | Radar2 |

# #VMP

```
VMP = Virtual Machine Protection = 虚拟机保护 = 虚拟软件保护技术 = 代码虚拟化

Android代码加固技术
软件保护壳

起源：老毛子的VmProtect(虚拟机保护)   
https://vmpsoft.com/
```

## ##指令虚拟化，软件保护壳的发展

```
第一阶段：当壳完成解密目标代码时，它将不会再次控制程序，被保护程序的明文将在内存中展开。在此之前，壳可以调用一切系统手段来防治黑客的调试与逆向

第二阶段：实现了分段式加解密，壳运行完毕后，并不会消失。等程序运行到某个节点时再次启动

第三阶段：将被保护的指令用一套自定义的字节码(逻辑上等价)来替换掉程序原有的指令，而字节码在执行的时候由程序中的解释器来解释执行，自定义的字节码只有自己的解释器才能识别。
```

## ##核心原理

```
代码虚拟化 = 基于Dalvik的解释器实现自己定义的指令

将程序代码编译为虚拟机指令即虚拟机代码(自己定义的代码集)，通过虚拟CPU解释并执行的一种方式

自定义一套虚拟机指令和对应的解释器，并将标准的指令转换成自己的指令，然后由解释器将自己的指令给对应的解释器
```

## ##例子

```
X86或arm体系架构的标准汇编指令(mov\add\pop等)，已变成了自定义加密汇编指令(xchg\db\dq等)
```

## ##图解

![image-20230726161356005](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726161356005.png)

## ##运行机制

![image-20230726161413354](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726161413354.png)

## ##运行流程

### ###运行流程·加固

![image-20230726161436870](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726161436870.png)

### ###运行流程·解释器

![image-20230726161454343](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726161454343.png)

## ##缺点

```
存在一定兼容性问题

会降低代码执行效率
```

## ##应用

**说明**

```
由于兼容性以及效率问题，故VMP一般只用于关键函数

根据保护的内容可分为dex的VMP和so的VMP

多数VMP的实现，是将smali翻译为C
```

**举例**

```
爱加密
提取dex中虚拟指令集，接着将dex中提取指令的方法清空，将方法修改为native方法，通过爱加密自定义指令替换规则，替换提取的指令并保存到其他文件中

通付盾
自定义指令集和自定义虚拟机运行环境的动态代码保护方案
```

## ##虚拟机

```
VMP的核心就是设计一个虚拟机，实现自定义指令的功能
```

**模块**

```
VM虚拟机

VM编译器

VM链接器

VM各种stub
```

**设计一个编译器**

![image-20230726161807114](C:\Users\Gintoki\AppData\Roaming\Typora\typora-user-images\image-20230726161807114.png)          

**编译器工作流程**

```
反汇编ARM

生成中间代码

处理定位

生成opcode
```

**实现一个基于虚拟机的保护壳，需完成**

```
随机VCode与Handle的关系映射

Handle混淆与乱序

代码变形

重定位
```

**参考资料**

```
https://github.com/eaglx/VMPROTECT
```

