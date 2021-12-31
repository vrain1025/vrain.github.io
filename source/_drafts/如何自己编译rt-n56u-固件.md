---
title: 如何自己编译rt-n56u 固件
tags: []
id: '527'
categories:
  - - 网络收集
---

关于在Ubuntu 16.04 TLS 中编译你自己路由的固件的说明。

1.  Install to your PC the [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads/).在你的电脑里面安装虚拟机环境，官方推荐的是免费的 [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads/) ，但你也可以使用vmware 或者其他的虚拟机系统安装。
2.  Download Ubuntu 16.04 LTS i386 (for example, [from this mirror](http://releases.ubuntu.com/releases/16.04/ubuntu-16.04-desktop-i386.iso)).下载 Ubuntu 16.04 LTS i386 光盘镜像，[点击这里过去](http://releases.ubuntu.com/releases/16.04/ubuntu-16.04-desktop-i386.iso)
3.  Create new virtual machine and install Ubuntu from step 2 to it. VirtualBox may use a ISO-image as drive in virtual machine.If you plan to use Ubuntu with the GUI, you must dedicate at least 1.5Gb of RAM for the virtual machine. When you select a smaller size of RAM you may receive errors when you create the image of the firmware.使用虚拟机管理工具一台新的虚拟机以及步骤2下载好的光盘镜像。大多数的虚拟机环境都可以支持直接把 iso 文件作为光盘载入。如果你打算使用ubuntu的GUI界面，内存最好设置为1.5G以上。如果你给虚拟机的内存太小了，在编译固件的时候，可能会出错。
4.  Start your virtual machine and open _Terminal_ on it.装好Ubuntu 以后，运行，进入终端。
5.  Install git:
    
    用以下指令安装 git。 sudo apt\-get update 
    sudo apt\-get install git
    
6.  Go to directory /opt and run command for create the local copy of repository:用以下步骤创建一个本地的源码副本：
    
    cd /opt
    sudo git clone https://bitbucket.org/padavan/rt-n56u.git
    
    This copies all the source code, creates a local git-repository. Directory /opt/rt-n56u will be the root of the git-repository. 这步会把整个源码目录复制回来建立本地的副本，目录 /opt/rt-n56u会是这个代码的根目录。
7.  Read the document /opt/rt-n56u/readme.eng.txt and install all the required packages that are listed in it:
    
    首先阅读/opt/rt\-n56u/readme.eng.txt 这个说明文档，然后安装编译固件所需的工具： sudo apt\-get install build\-essential gawk pkg\-config gettext automake autoconf libtool bison flex zlib1g\-dev libgmp3\-dev libmpfr\-dev libmpc\-dev texinfo python\-docutils mc
    
    mc (midnight commander) do not need to build the firmware, but it will help you navigate through directories, copy or edit files. mc 这个软件并不是必要的，但是用它来在源码目录中穿梭以及编辑，复制等操作都非常方便。
8.  Go to directory with toolchain sources (cross-compiler and tools for building) and build it:
    
    首先要编译一个交叉编译的工具链： cd /opt/rt\-n56u/toolchain\-mipsel
    sudo ./clean\_sources
    sudo ./build\_toolchain
    
    The result will be collected the target of toolchain /opt/rt-n56u/toolchain-mipsel/toolchain-3.4.x 编译好的工具链会存放在opt/rt-n56u/toolchain-mipsel/toolchain-3.4.x 这个目录中 If you plan to build the firmware with the kernel 3.0, you must build the appropriate version of tolchain: 默认的工具链是支持linux 3.4 内核模块的，如果你希望编译 linux 3.0 内核的，则必须按照以下方式编译出一个3.0 内核的工具链
    
    cd /opt/rt\-n56u/toolchain\-mipsel
    sudo ./clean\_sources
    sudo ./build\_toolchain\_3.0.x
    
    The result will be collected the target of toolchain /opt/rt-n56u/toolchain-mipsel/toolchain-3.0.x 这样编译好以后的工具链会放在 /opt/rt-n56u/toolchain-mipsel/toolchain-3.0.x 目录里面。 In the future, you will need these commands only if the toolchain will be updated. 在以后，仅仅在你需要更新或者升级工具链的情况下才需要重新处理这个步骤。
9.  Now go to directory with sources: 接下来让我们进入固件源码的目录：
    
    cd /opt/rt\-n56u/trunk
    
    and edit file /opt/rt-n56u/trunk/.config to fit your needs. 根据你的需要来自行编辑 /opt/rt-n56u/trunk/.config Edit path to toolchain (if you need it): 例如修改工具链的目录（仅仅在目录不一样的情况下）：
    
    CONFIG\_TOOLCHAIN\_DIR\=/opt/rt\-n56u/toolchain\-mipsel
    
    To build the firmware, for example, for router RT-N65U uncomment (remove the simbol #) the line: 然后把你需要编译的路由型号取消注释（删除#号）
    
    CONFIG\_FIRMWARE\_PRODUCT\_ID\="RT-N65U"
    
    and comment the line: 以及注释掉原来的那行。
    
    #CONFIG\_FIRMWARE\_PRODUCT\_ID="RT-N56U"
    
    Save the file after edit. 修改完成以后，记得保存文件。
10.  Clear source tree (every time before a new build) 在准备开始之前，我们还有一点工作要处理：清理源码树（基本上每次重新编译前都需要处理）
    
    sudo ./clear\_tree
    
11.  Build the firmware: 开始吧：
    
    sudo ./build\_firmware
    
    Created custom firmware file will be in the directory ./path\_to\_your\_dir/rt-n56u/trunk/images. If you want to save the firmware that you created earlier – copy it to another location, because the command clear\_tree overwrites the directory images. 你订制好的固件会存放在 /opt/rt-n56u/trunk/images 这个目录中。如果你想保存之前编译过的固件，记得每次编译好之后要把它复制出来，否则 clean\_tree指令会清空它。
12.  When [repository](https://bitbucket.org/padavan/rt-n56u/src) updated a local source tree must be updated with command: 当源码更新的时候，你需要在 rt-n56n的根目录中升级：
    
    sudo git pull
    
13.  If you made any changes to the local repository, when you upgrade tree some files could not be copied. In this case, you must give the command: 如果你修改过代码导致更新会出现冲突，这时候用以下的方式进行处理
    
    sudo git stash
    sudo git pull
    
14.  If toolchain sources (cross-compiler and tools for building) is changed you must re-build it: 如果工具链的代码更新了，你需要重新编译一个工具链：
    
    cd /opt/rt\-n56u/toolchain\-mipsel
    sudo ./clean\_sources  
    sudo ./clean\_toolchain  
    sudo ./build\_toolchain