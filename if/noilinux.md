# NoiLinux 2.0优化记录

NoiLinux 2.0在2021年7月16日从官网发布了，这个信息学奥赛的环境已经近十年没有更新了，现在基于ubuntu 20.04重新打包了一次，并且添加了一些新的功能。我也在主机上用hype-v安装了一个，使用中有一些必备的优化工作要记录下来，这些功能也与ubuntu 18.04的版本相通用。

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

## 获取 Qv2ray
要开始使用 Qv2ray，那就得先以某种方式获取到它。

我们提供了许多种方式，您可以根据您的喜好选择。

### 来自软件包管理器
#### Linux：Debian、Ubuntu 与它们的衍生版本
#### 安装相关工具

                sudo apt install gnupg ca-certificates curl

### 为 Debian 安装 Qv2ray 稳定版本

添加 Qv2ray 公钥到你的系统：

导入我们的 GPG 密钥，注意行尾的连字符。

                curl https://qv2ray.net/debian/pubkey.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/qv2ray-stable-archive.gpg

您还可以使用 FastGit 导入 GPG 公钥：

                curl https://raw.fastgit.org/Qv2ray/debian/master/pubkey.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/qv2ray-stable-archive.gpg

### 主存储库

添加我们的官方 APT 存储库：

Debian 稳定版：

                echo "deb [arch=amd64] https://qv2ray.net/debian/ stable main" | sudo tee /etc/apt/sources.list.d/qv2ray.list

如果您使用的是 Debian 不稳定版本，那么您需要改用此命令：

                echo "deb [arch=amd64] https://qv2ray.net/debian/ unstable main" | sudo tee /etc/apt/sources.list.d/qv2ray.list

更新 APT 索引：

                sudo apt update

您现在可以从 APT 安装 Qv2ray：

                sudo apt install qv2ray

### FastGit 镜像（用于加速下载 规避 GitHub 被墙）
添加我们的官方 APT 存储库：

                echo "deb [arch=amd64] https://raw.fastgit.org/Qv2ray/debian/master/ stable main" | sudo tee /etc/apt/sources.list.d/qv2ray-fastgit.list

如果您使用的是不稳定版本的 Debian，那么您需要改用此命令：

                echo "deb [arch=amd64] https://raw.fastgit.org/Qv2ray/debian/master/ unstable main" | sudo tee /etc/apt/sources.list.d/qv2ray-fastgit.list

更新 APT 索引：

                sudo apt update

您现在可以从 APT 安装 Qv2ray：

                sudo apt install qv2ray

### 适用于 Ubuntu 的 Qv2ray 稳定版

**注意：**所有的命令都要在bash中运行，如果你使用的是其他 shell，如zsh ， fish ，那么你需要先运行 bash命令。

将 Qv2ray 公钥添加到您的系统：

导入我们的 GPG 密钥，注意行尾的连字符：

                curl https://qv2ray.net/debian/pubkey.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/qv2ray-stable-archive.gpg

您还可以使用 FastGit 导入 GPG 公钥：

                curl https://raw.fastgit.org/Qv2ray/debian/master/pubkey.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/qv2ray-stable-archive.gpg

### 主存储库

添加我们的官方 APT 存储库：

                $ echo "deb [arch=amd64] https://qv2ray.net/debian/ `lsb_releases -cs` main" | sudo tee /etc/apt/sources.list.d/qv2ray.list

更新 APT 索引：

                sudo apt update

您现在可以从 APT 安装 Qv2ray：

                sudo apt install qv2ray

### FastGit 镜像（用于加速下载 规避 GitHub 被墙）

添加我们的官方 APT 存储库：

                $ echo "deb [arch=amd64] https://raw.fastgit.org/Qv2ray/debian/master/ `lsb_release` main" | sudo tee /etc/apt/sources.list.d/qv2ray-fastgit.list

更新 APT 索引：

                sudo apt update

您现在可以从 APT 安装 Qv2ray：

                sudo apt install qv2ray

注意： 如想要使用 Qv2ray 的开发版本，请阅读https://qv2ray.org/debian-dev (opens new window)， qv2ray-dev额外提供 Debian 的 arm64 和 mips64el 版本。如果您想使用，您应该将[arch=amd64]更改为您的架构，例如[arch=arm64] 。

## 安装 v2rayA
Debian 系列安装
### 方法一：通过软件源安装

添加公钥

        wget -qO - https://apt.v2raya.mzz.pub/key/public-key.asc | sudo apt-key add -

添加 V2RayA 软件源

        echo "deb https://apt.v2raya.mzz.pub/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list

        sudo apt update

安装 V2RayA

        sudo apt install v2raya

### 方法二：手动安装 deb 包

下载 deb 包后可以使用 Gdebi、QApt 等图形化工具来安装，也可以使用命令行：

        sudo apt install /path/download/installer_debian_xxx_vxxx.deb

 自行替换 deb 包所在的实际路径