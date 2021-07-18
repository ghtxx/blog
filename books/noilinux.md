# NoiLinux 2.0优化记录

NoiLinux 2.0在2021年7月16日总算从官网发布了，这个信息学奥赛的环境已经近十年没有更新了，现在基于ubuntu 18.04重新打包了一次，并且添加了一些新的功能。我也在主机上用hype-v安装了一个，使用中有一些必备的优化工作要记录下来，这些功能也与ubuntu 18.04的版本相通用。

## 启动SSH服务

        单次开启ssh

        sudo systemctl start ssh

        查看ssh是否启动，看到Active: active (running)即表示成功

        sudo systemctl status ssh

        开机自动启动ssh命令
        
        sudo systemctl enable ssh
        
        关闭ssh开机自动启动命令
        
        sudo systemctl disable ssh
        
        单次关闭ssh

        sudo systemctl stop ssh

        设置好后重启系统
        
        reboot

由于系统中已经默认安装了openssh server就不用再执行

        apt-get install openssh-server

进行单独的安装操作了。直接用上面的命令执行就可以了。

## 默认登录的用户名和密码

即安装过程中设置的用户名与密码，root密码可以使用

    sudo passwd root

进行修改，修改后可本机登录，但ssh登录时root不可使用密码，要使用密钥登录。

## 关闭屏保与锁屏

个人使用完全不需要这个功能，在设置中对电源以及隐私中的锁屏做一下设置就好。

## 建议的系统配置
内存：8G 当然最好了，不过最小使用2G也可以运行。CPU越强当然越节省时间。

默认的浏览器是火狐，非常好用，建议开启同步，方便学习。

dock上只有火狐和文件管理器，建议将终端、编辑器和本机测评系统Arbiter放到dock上。

## 比赛语言
目前的比赛语言还是只有3种：C、C++、Pascal，这个不知道是不是比赛规则的问题，我觉得Python是比较好的选择。虽然系统中内置了pythone2和3的支持，但2021年来看还不提供这两种语言参赛。

建议初学者从C++开始吧，因为C++的编译器更容易掌握。

## 更改ssh服务端口
默认的22端口通常来说会有被扫描的风险，而且多机器使用时也不太方便，变更成另一个不常用的端口会更方便一点，执行下面的命令：

        sudo  vi /etc/ssh/sshd_config

修改 #Port 22 为 Port **自己喜欢的端口号** 就行了。
