# openSuSe的优化记录

将使用opensuse的过程中做的一些重要问题加以记录。

## 科大的源
opensuse官方源国内访问有问题，只好换成了科大的源：

        https://mirrors.ustc.edu.cn/opensuse/tumbleweed/repo/oss/

可参考官方的一个[文档说明](https://zh.opensuse.org/SDB:%E6%B7%BB%E5%8A%A0%E8%BD%AF%E4%BB%B6%E6%BA%90#.E6.B7.BB.E5.8A.A0.E9.95.9C.E5.83.8F.E6.BA.90)

## 系统软件安装方法

opensuse的安装软件命令又不一样了，比如安装git要这样：

        zypper in git-core

## 中文的设置方式

在 Yast 的 Language 配置中将中文加入，可以把简体中文（Simplified Chinese）选择为第二语言（Secondary Language），确认之后，系统会自动下载语言相关的组件和字体，注销当前登录之后生效。不过我还是把中文设成主语言了。相应的其他功能都会自动到位，比如liboffice的中文界面，输入法什么的都很快安装好了。

## opensuse的支持网站

使用nvdia的显卡：https://en.opensuse.org/SDB:NVIDIA_drivers 不过我的电脑是集显的，就不测试这个了。

opensuse的版本非常多，免费个人用户直接用Leap版本就好了。各版本的发行状况都是公开的：https://build.opensuse.org/monitor

官方文档在这：https://doc.opensuse.org/ 有[中文版](https://doc.opensuse.org/zh-CN/)

## 安装atom

从官网下载rpm包直接安装是个简单快捷的办法：

      sudo rpm -ivh ./atom.x86_64.rpm

如果没有LSB会出错误：依赖检测失败：
    lsb-core-noarch 被 atom-1.57.0-0.1.x86_64 需要

LSB是linux基本包的缩写，有时候定制安装会没有选上，这就要费点事了，走合适的源安装补上就行了：https://software.opensuse.org/package/lsb?locale=zh_TW

## sshd服务默认没开
要用root帐号手动启动一下：

        systemctl start sshd

要开机自动启动sshd就要设置：

        systemctl enable sshd

参考：[国外的一个指导文档](https://www.cyberithub.com/how-to-start-and-enable-sshd-service-in-opensuse-linux/#:~:text=How%20to%20Enable%20SSHD%20Service%20on%20OpenSUSE%20Linux,to%20manually%20start%20the%20Service%20after%20every%20reboot)

## ssh出现能连接不能登录的问题
端口是正常的，可以连接，但输入正确密码也无法登录，原因不明，怀疑是当时在使用ssh的同时做了更新造成了什么冲突。

## 外观
kde是最好看的，有点儿苹果的感觉；gnome跟ubuntu差不多;xfce是最简洁的，早期linux的感觉。

先安装了gnome的时候也是可以再安装kde的，执行这个命令：

    zypper install -t pattern kde kde_plasma

不过两个窗口都使用似乎稳定性会下降，当然，也可能是因为我在KDE里面安装了太多图标包和窗口动画的原因。最重要的还有一个问题就是在GNOME中安装的ATOM到了KDE里面就无法启动了，原因不明。

官方的建议在[这里](https://zh.opensuse.org/SDB:KDE_%E5%AE%89%E8%A3%85)

两种窗口都存在的时候，登录时选择的上一个会被记为默认。

## 安装vs code的最佳方法

执行几个命令就行了，微软对开源的拥抱真的很棒：

    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

引入微软的密钥。

    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'

加入微软的repo源。

     sudo zypper refresh
     sudo zypper install code

刷新并安装code编码器！

## 安装chrome稳定版

添加Chrome存储库

第一步是添加Google Chrome存储库。启动终端并运行以下命令。

    sudo zypper ar http://dl.google.com/linux/chrome/rpm/stable/x86_64 Google-Chrome

在命令中，“ ar”代表“ addrepo”。要了解有关Zypper及其用法的更多信息，请查看[如何在openSUSE上使用Zypper](https://translate.googleusercontent.com/translate_c?depth=1&pto=aue&rurl=translate.google.ac&sl=en&sp=nmt4&tl=zh-CN&u=https://linuxhint.com/opensuse_package_manager/&usg=ALkJrhiEwty3w0hUk8euI_LBNzw2aSjiyA)。

该仓库尚未准备就绪，无法使用。我们需要添加Google公共签名密钥，以便可以对软件包进行验证。运行这些命令。
wget https://dl.google.com/linux/linux_signing_key.pub

    sudo rpm --import linux_signing_key.pub

密钥导入完成后，更新zypper的回购缓存。

    sudo zypper ref -f


最后，安装Chrome，zypper准备从存储库中获取Google Chrome！

    sudo zypper in google-chrome-stable
