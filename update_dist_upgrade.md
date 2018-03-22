## 0. Ubuntu 16.04系统下出现

>E: 无法下载 http://ppa.launchpad.net/fcitx-team/nightly/ubuntu/dists/xenial/main/binary-amd64/Packages 404 Not Found

解决方案：删除对应的ppa

步骤如下：

1.切换到对应的ppa目录下
`cd /etc/apt/sources.list.d`

2.ls查看文件
删除`fcitx-team-ubuntu-nightly-xenial.list`即可（为了安全起见，可以进行添加后缀.bak的备份）

 `mv fcitx-team-ubuntu-nightly-xenial.list fcitx-team-ubuntu-nightly-xenial.list.bak `



## 1. apt-update
用户使用apt-get update更新。这样，apt-get才能知道每个软件包的最新信息，从而正确地下载最新版本的软件。

至于apt-get upgrade，则是对已经安装的软件包本身进行更新的过程。由于确定要更新的软件包需要对本地安装的版本和列表的版本进行比较，所以要在update以后运行这一条。
要求在install操作之前执行update和upgrade，实际上是确保本地软件列表信息和已安装软件均为最新的过程。这样做可以最大限度地确保新安装的软件包正常工作。

一般来说，update和upgrade不需要每次安装软件之前都运行，安装新软件的话一天左右运行一次即可，不安装软件的时候隔十天半个月运行一下来更新软件包，服务器系统如果没有安全性更新就别乱更新了，稳定最重要。

PS：软件源服务器地址可以在/etc/apt/sources.list里面看到。

## 2. apt-get upgrade和dist-upgrade的差别

upgrade:系统将现有的Package升级,如果有相依性的问题,而此相依性需要安装其它新的Package或影响到其它Package的相依性时,此Package就不会被升级,会保留下来。

dist-upgrade:可以聪明的解决相依性的问题,如果有相依性问题,需要安装/移除新的Package,就会试着去安装/移除它. (所以通常这个会被认为是有点风险的升级) 

apt-get upgrade 和 apt-get dist-upgrade 本质上是没有什么不同的。只不过，**dist-upgrade 会识别出当依赖关系改变的情形并作出处理，而upgrade对此情形不处理。**

>例如软件包 a 原先依赖 b c d，但是在源里面可能已经升级了，现在是 a 依赖 b c e。这种情况下，dist-upgrade 会删除 d 安装 e，并把 a 软件包升级，而 upgrade 会认为依赖关系改变而拒绝升级 a 软件包。
