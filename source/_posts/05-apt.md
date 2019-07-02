---
title: 软件包管理系统
date: 2019-03-28 13:05:06
tags: [linux,ubuntu]
categories: GeekCoder
---

2019-03-28
**[GeekCoder]**,***linux***,***ubuntu***

### 历史背景
****
起初GNU/Linux系统中只有.tar.gz。用户 必须自己编译他们想使用的每一个程序。在Debian出现后，人们认为有必要在系统 中添加一种机 制用来管理 安装在计算机上的软件包。
人们将这套系统称为 [dpkg](https://zh.wikipedia.org/zh-cn/Dpkg)。至此着名的package首次在GNU/Linux上出现。不久之後红帽子也开始着手建立自己的包管理系统 [rpm](https://zh.wikipedia.org/wiki/RPM%E5%A5%97%E4%BB%B6%E7%AE%A1%E7%90%86%E5%93%A1)。

GNU/Linux的创造者们很快又陷入了新的窘境。他们希望通过一种快捷、实用而且高效的方式来安装软件包。这些软件包可以自动处理相互之间 的依赖关系，并且在升级过程中维护他们的配置文件 。Debian又一次充当了开路先锋的角色。它首创了APT（Advanced Packaging Tool）。这一工具后来被Conectiva 移植到红帽子系统中用于对RPM包的管理。在其他一些发行版中我们也能看到它的身影。

### 简介
****
**软件包管理系统**是在计算机中自动安装、配制、卸载和升级软件包的工具组合，在各种系统软件和应用软件的安装管理中均有广泛应用。
在Linux发行版中，几乎每一个发行版都有自己的软件包管理系统。常见的有：
- 管理deb(debian package)软件包的dpkg以及它的前端apt（使用于Debian、Ubuntu）。
> deb是Debian软件包格式，文件扩展名为.deb。Debian包是Unixar的标准归档，将包文件信息以及包内容，经过gzip和tar打包而成。处理这些包的经典程序是dpkg，经常是通过apt来运作。
- RPM软件包管理器(Red-Hat Package Manager)以及它的前端dnf（使用于Fedora）、前端yum（使用于Red Hat Enterprise Linux）、前端ZYpp（使用于openSUSE）、前端urpmi（使用于Mandriva Linux、Mageia）等。
> 一种用于互联网下载包的打包及安装工具，它包含在某些Linux分发版中。它生成具有.RPM扩展名的文件。与Dpkg类似。

**使用软件包管理系统将大大简化在Linux发行版中安装软件的过程。**
`dpkg`和`rpm`都提供很多实用的命令，例如安装、卸载和升级，查询已安装的软件包。

### dpkg和apt-get的区别与联系
****
两者的**区别**是dpkg绕过apt包管理数据库对软件包进行操作，所以你用dpkg安装过的软件包用apt可以再安装一遍，系统不知道之前安装过了，将会覆盖之前dpkg的安装。
1.  dpkg是用来安装.deb文件,但不会解决模块的依赖关系,且不会关心ubuntu的软件仓库内的软件,可以用于安装本地的deb文件。
2.  apt会解决和安装模块的依赖问题,并会咨询软件仓库, 但不会安装本地的deb文件, apt是建立在dpkg之上的软件管理工具。

dpkg使用文本文件作为数据库（/var/lib/dpkg）来维护系统中的软件，包括软件的依赖关系、软件状态等详细信息。 apt-get源的配置：修改/etc/apt/sources.list 文件 

> **查询**
> `dpkg -l` 列出系统中所有安装的包 
> `dpkg -s package-name` 查询系统中某个软件包的详细信息 
> `dpkg -L package-name` 显示已安装软件包的文件列表 
> `dpkg -S file` 查询系统中指定的文件属于哪个包
> **安装软件包**
> `dpkg -i package_name.deb`      //安装本地软件包，不解决依赖关系
> `apt-get install package`      //在线安装软件包
> `aptitude install patter`      //同上
> `apt-get install package --reinstall`      //重新安装软件包
> `apitude reinstall package`      //同上
> **移除软件包**
> `dpkg -r package`      //删除软件包
> `apt-get remove package`      //卸载软件
> `aptitude remove package`      //同上
> `dpkg -P package`      //删除软件包及配置文件
> `apt-get remove package --purge`      //删除软件包及配置文件
> `apitude purge pattern`      //同上
> **其他**
> `apt-get update`      //刷新存储库索引
> `apt-get upgrade`      //更新所有已安装的软件包 
> `apt-get dist-upgrade`      //将系统升级到新的发行版
> `apt-get autoremove`      //自动删除不需要的包

### aptitude 与 apt-get 的区别与联系
****
在基于 Debian 的 Linux 发行版中，有各种工具可以与 APT 进行交互，以方便用户安装、删除和管理的软件包。apt-get 便是其中一款广受欢迎的命令行工具，另外一款较为流行的是 [Aptitude](https://wiki.debian.org/Aptitude?action=show&redirect=aptitude) 这一命令行与 GUI 兼顾的小工具。

aptitude 与 apt-get 一样，是 Debian 及其衍生系统中功能极其强大的包管理工具。与 apt-get 不同的是，aptitude 在处理依赖问题上更佳一些。举例来说，aptitude 在删除一个包时，会同时删除本身所依赖的包。这样，系统中不会残留无用的包，整个系统更为干净。
** 由于aptitude比apt-get了解更多信息，可以说它更适合用来进行安装和卸载。**

有的问题 apt-get 解决不了，必须使用 aptitude 解决，有的问题，用 aptitude 解决不了，必须使用 apt-get。
- aptitude 解决得更好的地方： install, remove, reinstall（apt-get无此功能）, show（apt-get无此功能）, search（apt-get无此功能）, hold（apt-get无此功能）, unhold（apt-get无此功能）,
- apt-get 解决得更好的地方： source（aptitude无此功能）, build-dep （低版本的aptitude没有build-dep功能）。
- apt-get 跟 aptitude 没什么区别的地方：update, upgrade (apt-get upgrade == aptitude safe-upgrade, apt-get dist-upgrade == aptitude full-upgrgade)。

### apt-get和apt区别
****
Ubuntu 16.04 发布时，一个引人注目的新特性便是 apt 命令的引入。其实早在 2014 年，apt 命令就已经发布了第一个稳定版，只是直到 2016 年的 Ubuntu 16.04 系统发布时才开始引人关注。
随着 `apt install package`命令的使用频率和普遍性逐步超过` apt-get install package`，越来越多的其它 Linux 发行版也开始遵循 Ubuntu 的脚步，开始鼓励用户使用 apt 而不是 apt-get。
#### apt与apt-get
如果你已阅读过 **apt-get 命令指南**，可能已经遇到过许多类似的命令，如`apt-cache`、`apt-config` 等。如你所见，这些命令都比较低级又包含众多功能，普通的 Linux 用户也许永远都不会使用到。换种说法来说，就是最常用的 Linux 包管理命令都被分散在了` apt-get`、`apt-cache` 和 `apt-config` 这三条命令当中。
apt 命令的引入就是为了解决命令过于分散的问题，它包括了 apt-get 命令出现以来使用最广泛的功能选项，以及 apt-cache 和 apt-config 命令中很少用到的功能。
在使用 apt 命令时，用户不必再由 apt-get 转到 apt-cache 或 apt-config，而且 apt 更加结构化，并为用户提供了管理软件包所需的必要选项。
> 简单来说就是：apt = apt-get、apt-cache 和 apt-config 中最常用命令选项的集合。

#### apt和apt-get命令之间的区别
虽然 apt 与 apt-get 有一些类似的命令选项，但它并不能完全向下兼容 apt-get 命令。也就是说，可以用 apt 替换部分 apt-get 系列命令，但不是全部。
|     apt命令      |      取代的命令      |           命令的功能           |
| :--------------: | :------------------: | :----------------------------: |
|   apt install    |   apt-get install    |           安装软件包           |
|    apt remove    |    apt-get remove    |           移除软件包           |
|    apt purge     |    apt-get purge     |      移除软件包及配置文件      |
|    apt update    |    apt-get update    |         刷新存储库索引         |
|   apt upgrade    |   apt-get upgrade    |     升级所有可升级的软件包     |
|  apt autoremove  |  apt-get autoremove  |       自动删除不需要的包       |
| apt full-upgrade | apt-get dist-upgrade | 在升级软件包时自动处理依赖关系 |
|    apt search    |   apt-cache search   |          搜索应用程序          |
|     apt show     |    apt-cache show    |           显示装细节           |

当然，apt 还有一些自己的命令：
|   新的apt命令    |              命令的功能              |
| :--------------: | :----------------------------------: |
|     apt list     | 列出包含条件的包（已安装，可升级等） |
| apt edit-sources |              编辑源列表              |
需要大家注意的是：`apt` 命令也还在不断发展， 因此，你可能会在将来的版本中看到新的选项。

### 致谢和参考资料
****
[1]作者未考.[软件包管理系统](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E5%8C%85%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F).来源:维基百科,时间未考
[2]wsclinux.[dpkg和apt-get的区别与联系](https://blog.csdn.net/wsclinux/article/details/69501992).来源:CSDN,2017.04.07
[3]lose_wait.[dpkg 和 apt-get的使用](https://blog.csdn.net/u012012939/article/details/48465185).来源:CSDN,2015.09.15
[4]Debian社区.[aptitude 与 apt-get 的区别与联系](https://cloud.tencent.com/developer/article/1374705).来源:腾讯云,2018.12.20
[4]作者未考.[Linux中apt与apt-get命令的区别与解释](https://www.sysgeek.cn/apt-vs-apt-get/).来源:系统极客,2017.07.09