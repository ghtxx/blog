# windows通用指令

windows系统的向下兼容是做的最好的，毕竟是大厂作品，没有linux各发行版互不兼容的毛病，在指令的使用上更是保持了与20年前发行的xp都兼容的高水准，不得不佩服，这里记录一些实用的指令。通常都是用win键+R来运行它们的。通常可在cmd中执行。

windows的指令不区分大小写，这一点与linux的差别很大，使用多系统时要注意这个问题。

## 自动登录

                control userpasswords2

在多用户的系统变成自己专用设备时使用这个命令可以避免开机后要输入密码登录的问题。

                Rundll32 netplwiz.dll,UsersRunDll

同样的效果，不过这个命令在server版上使用较多。

## 重启远程计算机的DOS命令

                shutdown /?

用法: shutdown [-i | -l | -s | -r | -a] [-f] [-m \\computername] [-t xx] [-c "co
mment"] [-d up:xx:yy]

没有参数 显示此消息(与 ? 相同)

-i 显示 GUI 界面，必须是第一个选项

-l 注销(不能与选项 -m 一起使用)

-s 关闭此计算机

-r 关闭并重启动此计算机

-a 放弃系统关机

-m \\computername 远程计算机关机/重启动/放弃

-t xx 设置关闭的超时为 xx 秒

-c "comment" 关闭注释(最大 127 个字符)

-f 强制运行的应用程序关闭而没有警告

-d [p]:xx:yy 关闭原因代码

u 是用户代码

p 是一个计划的关闭代码

xx 是一个主要原因代码(小于 256 的正整数)

yy 是一个次要原因代码(小于 65536 的正整数)

比如重启IP地址为192.168.1.2的电脑：

                shutdown -r -m \\192.168.1.2

## win7启用休眠功能

只需要执行一条

        powercfg -h on


 
## 最基本,最常用的,测试物理网络的

        ping 192.168.0.8 -t 

参数-t是等待用户去中断测试

## 查看DNS、IP、Mac等

　　A.Win98:winipcfg

　　B.Win2000以上:

        Ipconfig/all

## NSLOOKUP:

如查看河北的DNS

        C:\>nslookup
        Default Server: ns.hesjptt.net.cn
        Address: 202.99.160.68
        >server 202.99.41.2 则将DNS改为了41.2
        > pop.pcpop.com
        Server: ns.hesjptt.net.cn
        Address: 202.99.160.68

　　Non-authoritative answer:
　　Name: pop.pcpop.com
　　Address: 202.99.160.212

## 网络信使 
一种早期版本中自动在对方机器上显示信息的方法：

        Net send
        
计算机名/IP* (广播) 传送内容,注意不能跨网段

        net stop messenger
        
停止信使服务,也可以在面板-服务修改

        net start messenger
        
开始信使服务

## 探测对方

包括对方计算机名,所在的组、域及当前用户名 (当年著名软件《追捕》的工作原理)

        ping -a IP -t 

只显示NetBios名

　　nbtstat -a 192.168.10.146

比较全的

## netstat

        netstat -a
        
显示出你的计算机当前所开放的所有端口

        netstat -s -e
        
比较详细的显示你的网络资料,包括TCP、UDP、ICMP 和 IP的统计等

## 探测arp绑定(动态和静态)列表

显示所有连接了我的计算机,显示对方IP和MAC地址

        arp -a

在代理服务器端捆绑IP和MAC地址,解决局域网内盗用IP!:

        ARP -s 192.168.10.59 00 -50-ff-6c-08-75

解除网卡的IP与MAC地址的绑定:

        arp -d 网卡IP

## 在网络邻居上隐藏你的计算机 (让人家看不见你!)

        net config server /hidden:yes

重新开启显示指令：

        net config server /hidden:no
        
 
## 几个net命令

### 显示当前工作组服务器列表

        net view
 
 当不带选项使用本命令时,它就会显示当前域或网络上的计算机上的列表。
　　比如:查看这个IP上的共享资源,就可以

        C:\>net view 192.168.10.8

　　在 192.168.10.8 的共享资源
　　资源共享名 类型 用途 注释
　　--------------------------------------
　　网站服务 Disk
　　命令成功完成。

### 查看计算机上的用户帐号列表

        net user

### 查看网络链接

        net use

　　例如:net use z: \\192.168.10.8\movie 将这个IP的movie共享目录映射为本地的Z盘

### 记录链接 net session

　　例如:

        C:\>net session

　　计算机 用户名 客户类型 打开空闲时间
　　-------------------------------------------------------------------------------
　　\\192.168.10.110 ROME Windows 2000 2195 0 00:03:12

　　\\192.168.10.51 ROME Windows 2000 2195 0 00:00:39
　　命令成功完成。

## 路由跟踪命令


### 基本命令 tracert

        tracert pop.pcpop.com

### pathping

pathping pop.pcpop.com 除了显示路由外,还提供325S的分析,计算丢失包的%

## 关于共享安全的几个命令

### 查看你机器的共享资源

        net share

### 手工删除共享

可以编个bat文件,开机自运行,把共享都删了!

        net share c$ /d
        net share d$ /d
        net share ipc$ /d
        net share admin$ /d

　　注意$后有空格。

### 增加一个共享:

        c:\net share mymovie=e:\downloads\movie /users:1

mymovie 共享成功，同时限制链接用户数为1人。

## 在DOS行下设置静态IP

### 设置静态IP
　　
        CMD
        netsh
        netsh>int
        interface>ip
        interface ip>set add "本地链接" static IP地址 mask gateway

### 查看IP设置

        interface ip>show address

## Arp

　 　显示和修改“地址解析协议 (ARP)”缓存中的项目。ARP 缓存中包含一个或多个表,它们用于存储 IP 地址及其经过解析的以太网或令牌环物理地址。计算机上安装的每一个以太网或令牌环网络适配器都有自己单独的表。如果在没有参数的情况下使用,则 arp 命令将显示帮助信息。

### 语法

        arp [-a [InetAddr] [-N IfaceAddr]] [-g [InetAddr] [-N IfaceAddr]] [-d InetAddr [IfaceAddr]] [-s InetAddr EtherAddr [IfaceAddr]]

### 参数

        -a [InetAddr] [-N IfaceAddr]


    显示所有接口的当前 ARP 缓存表。要显示指定 IP 地址的 ARP 缓存项,请使用带有 InetAddr 参数的 arp -a,此处的 InetAddr 代表指定的 IP 地址。要显示指定接口的 ARP 缓存表,请使用 -N IfaceAddr 参数,此处的 IfaceAddr 代表分配给指定接口的 IP 地址。-N 参数区分大小写。

        -g [InetAddr] [-N IfaceAddr]

    与 -a 相同。

        -d InetAddr [IfaceAddr]

    删除指定的 IP 地址项,此处的 InetAddr 代表 IP 地址。对于指定的接口,要删除表中的某项,请使用 IfaceAddr参数,此处的 IfaceAddr 代表分配给该接口的 IP 地址。要删除所有项,请使用星号 (*) 通配符代替 InetAddr。

        -s InetAddr EtherAddr [IfaceAddr]

    向 ARP 缓存添加可将 IP 地址 InetAddr 解析成物理地址 EtherAddr 的静态项。要向指定接口的表添加静态 ARP 缓存项,请使用 IfaceAddr 参数,此处的 IfaceAddr 代表分配给该接口的 IP 地址。

        /?

    在命令提示符显示帮助。


### 注释

　　InetAddr 和 IfaceAddr 的 IP 地址用带圆点的十进制记数法表示。

　　物理地址 EtherAddr 由六个字节组成,这些字节用十六进制记数法表示并且用连字符隔开(比如,00-AA-00-4F-2A-9C)。

　　通过 -s 参数添加的项属于静态项,它们不会 ARP 缓存中超时。如果终止 TCP/IP 协议后再启动,这些项会被删除。要创建永久的静态 ARP 缓存项,请在批处理文件中使用适当的 arp 命令并通过“计划任务程序”在启动时运行该批处理文件。

　　只有当网际协议 (TCP/IP) 协议在 网络连接中安装为网络适配器属性的组件时,该命令才可用。

### 范例

　　要显示所有接口的 ARP 缓存表,可键入:

        arp -a

　　对于指派的 IP 地址为 10.0.0.99 的接口,要显示其 ARP 缓存表,可键入:

        arp -a -N 10.0.0.99

　　要添加将 IP 地址 10.0.0.80 解析成物理地址 00-AA-00-4F-2A-9C 的静态 ARP 缓存项,可键入:

        arp -s 10.0.0.80 00-AA-00-4F-2A-9C 