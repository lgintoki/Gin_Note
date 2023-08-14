# #Command

## ⼀、msfconsole

```shell
back 从当前环境返回
banner  显⽰⼀个MSF banner
cd  切换⽬录
color  颜⾊转换
connect  连接⼀个主机
exit  退出MSF
help  帮助菜单
info  显⽰⼀个或多个模块的信息
irb  进⼊irb脚本模式
jobs  显⽰和管理作业
kill  杀死⼀个作业
load  加载⼀个插件
loadpath 在⼀个路径搜索并加载模块
quit  退出MSF
resource 运⾏存储在⼀个⽂件中的命令
route  查看⼀个会话的路由信息
save  保存动作
search  搜索模块名和描述
set  给⼀个变量赋值
setg  把⼀个值赋给全局变量
show  显⽰所给类型的模块，或所有模块
sleep  在限定的秒数内什么也不做
unload  卸载⼀个模块
unset  解除⼀个或多个变量
unsetg  解除⼀个或多个全局变量
use  通过名称选择⼀个模块
version  显⽰MSF和控制台库版本号
```



## ⼆、database

```shell
db_add_host 添加⼀个或多个主机到数据库
db_add_note 添加⼀个注释到主机
db_add_port 添加⼀个端⼝到主机
db_connect 连接⼀个存在的数据库
db_create 创建⼀个新的数据库实例
db_del_host 从数据库删除⼀个或多个主机
db_del_port 从数据库删除⼀个端⼝
db_destroy 删除⼀个存在的数据库
db_disconnect 断开与当前数据库实例的连接
db_driver 指定⼀个数据库驱动
db_hosts 列出数据库中的所有主机
db_nmap  执⾏Nmap并记录输出
db_notes 列出数据库中的所有注释
db_services 列出数据库中的所有服务
db_vulns 列出数据库中的所有漏洞
db_workspace 转换数据库⼯作区
db_import_ip_list 引⼊⼀个IP列表⽂件
db_import_amap_mlog 引⼊⼀个THC-Amap扫描结果⽂件(-o -m)
db_import_nessus_nbe 引⼊⼀个Nessus扫描结果⽂件(NBE)
db_import_nessus_xml 引⼊⼀个Nessus扫描结果⽂件
db_import_nmap_xml 引⼊⼀个Nmap扫描结果⽂件(-oX)
db_autopwn ⾃动利⽤
```



## 三、db_autopwn

```shell
-h 显⽰帮助
-t 显⽰所有匹配的利⽤模块
-x 选择基于漏洞的模块
-p 选择基于开放端⼝的模块
-e 运⾏所有匹配⽬标的利⽤程序
-r ⽤⼀个反向连接的shell(reverse)
-b ⽤⼀个随机端⼝的绑定shell(bind)
-q 禁⽤利⽤程序输出
-l [范围] 只对此范围内的主机进⾏利⽤
-X [范围] 永远排除此范围内的主机
-PI [范围] 只对开放这些的端⼝的主机进⾏利⽤
-PX [范围] 永远排除对开放这些端⼝的主机
-m [范围] 只运⾏名字与正则表达式匹配的模块
```



## 四、Meterpreter

**核⼼命令：**

```shell
channel  显⽰动态频道的信息
close  关闭⼀个频道
exit  终⽌meterpreter会话
help  帮助菜单
interact 频道交互
irb  IRB脚本模式
migrate  转移meterpreter到其他进程
quit  终⽌meterpreter
read  从频道读数据
run  执⾏⼀个meterpreter脚本
use  加载⼀个或多个扩展
write  向频道写数据
```

**⽂件系统命令：**

```shell
cat  读取⼀个⽂件内容到屏幕
cd  切换⽬录
del  删除指定⽂件
download 下载⼀个⽂件或⽬录
edit  编辑⼀个⽂件
getlwd  获取本地⼯作⽬录
getwd  切换⼯作⽬录
lcd  切换本地⼯作⽬录
lpwd  打印本地⼯作⽬录
ls  ⽂件列表
mkdir  创建⽬录
pwd  打印当前⼯作⽬录
rm  删除指定⽂件
rmdir  远程⽬录
upload  上传⼀个⽂件或⽬录
```

**⽹络命令：**

```shell
ipconfig 显⽰⽹络接⼝
portfwd  发送⼀个本地端⼝到⼀个远程服务
route  查看和修改路由表
```

**系统命令：**

```shell
clearev  清除事件⽇志
execute  执⾏⼀个命令
getpid  取得当前进程ID
getuid  取得服务器运⾏⽤户
kill  杀死⼀个进程
ps  列出进程列表
```



## 五、Metasploit Database ManageCommand（数据库管理命令）

```shell
msfdb init：启动并初始化数据库
msfdb reinit：删除并重新初始化数据库
msfdb delete：停止使用数据库并且删除
msfdb run：启动数据库并运行msfconsole
msfdb start：启动数据库
msfdb stop：停止数据库
msfdb status：检查服务状态 
```



## 六、Metasploit Core Commands（核心命令）

```shell
?：帮助菜单
banner：显示Metasploit旗标信息
cd：更改当前工作目录
color：切换颜色
connect：与主机通信
exit：退出控制台
get：获取特定变量的值
getg：获取全局变量的值
grep：搜索另一个命令的输出
help：帮助菜单
history：显示命令历史记录
load：加载框架插件
quit：退出控制台
repeat：重复一个命令列表
route：通过会话路由流量
save：保存活动数据存储
sessions：显示会话列表和信息
set：设置一个变量的值
setg：设置一个全局变量的值
sleep：在指定的秒数内不执行任何操作
spool：将控制台输出写入文件以及屏幕
threads：查看和操作后台线程
unload：卸载框架插件
unset：取消设置的一个或多个变量
unsetg：取消设置一个或多个全局变量
version：显示框架和控制台库版本号 
```



## 七、Metasploit Module Commands（模块命令）

```shell
advanced：显示一个或多个模块的高级选项
back：从当前环境返回
info：显示一个或多个模块的详细信息
loadpath：从路径中搜索并加载模块
options：显示全局选项或一个或多个模块
popm：使其主动从堆栈弹出新的模块
previous：将先前加载的模块设置为当前模块
pushm：将活动模块或模块列表推送到模块堆栈
reload_all：重新加载所有模块
search：搜索模块名称和描述
show：显示给定类型的的模块或所有模块
use：按名称选择模块 
```



## 八、Metasploit Job、Script Commands（作业、脚本命令）

```shell
makerc：保存从开始时输入的命令到一个文件
resource：运行存储在一个文件中的命令
handler：将有效载荷处理程序作为作业启动
jobs：显示和管理作业
kill：杀死一个作业
rename_job：重命名作业 
```



## 九、Metasploit Database Backend Commands（后端数据库命令）

```shell
analyze：分析有关特定地址或地址范围的数据库信息
db_connect：连接到现有数据服务
db_disconnect：断开与当前数据服务的连接
db_export：导出包含数据库内容的文件
db_import：导入扫描结果文件（将自动检测文件类型）
db_nmap：执行nmap并自动记录输出
db_rebuild_cache：重建数据库存储的模块高速缓存
db_remove：删除已保存的数据服务条目
db_save：将当前数据服务连接保存为启动时重新连接的默认值
db_status：显示当前数据库服务状态
creds：列出数据库中的所有凭证
hosts：列出数据库中的所有主机
loot：列出所有数据库中的战利品
notes：列出数据库中的所有记录
services：列出数据库中的所有服务
vulns：列出数据库中的所有漏洞
workspace：在数据库工作区之间切换 
```



## 十、Metasploit Developer、Exploit Commands（开发、利用命令）

```shell
edit：使用首选编辑器编辑当前模块或文件
irb：打开交互式Ruby shell
log：如果可能，显示frame.log分页到最后
pry：在当前模块或框架上打开Pry调试器
reload_lib：从指定路径重新加载Ruby库文件
check：检查目标是否容易受到攻击
exploit：启动漏洞利用尝试
rcheck：重新加载模块并检查目标是否易受攻击
recheck：重新检查rcheck的别名
reload：重新加载指定模块
rerun：重新运行rexploit的别名
rexploit：重新加载模块并启动漏洞利用尝试
run：运行别名以进行利用 
```

#  #More

