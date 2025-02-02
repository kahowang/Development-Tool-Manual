.. role:: raw-html-m2r(raw)
   :format: html


Hareware&&Kernel
================

监控资源
--------

进程
^^^^

htop(进程)
~~~~~~~~~~

一般查看当前用户下最占用cpu（P）和内存（M）的进程


* 命令行

.. prompt:: bash $,# auto

   # 只查看当前用户的进程
   $ htop -u $(whoami)


* 交互式快捷键

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210904001431390.png" alt="image-20210904001431390" style="zoom:50%; " />`


* 配置项

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210904002516344.png" alt="image-20210904002516344" style="zoom:67%; " />`

查看进程树
~~~~~~~~~~


* 图形化界面（for KDE）

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210910181315174.png" alt="image-20210910181315174" style="zoom:50%; " />`


* `命令行 <https://www.howtoforge.com/linux-pstree-command/>`_

.. prompt:: bash $,# auto

   $ pstree [user]
   -s：查看指定pid的父进程
   -u：显示user
   -p：显示pid号
   -T：隐藏线程
   -t：显示线程全称
   -a：显示对应的命令行
   -g：显示组ID

综合
~~~~

zenith
^^^^^^


* 可从\ `此处 <https://github.com/bvaisvil/zenith/releases>`_\ 下载相应的deb包(e.g. zenith_0.12.0-1_amd64.deb)

.. prompt:: bash $,# auto

   $ cd ~/application
   $ wget -c https://github.com/bvaisvil/zenith/releases/download/0.12.0/zenith_0.12.0-1_amd64.deb
   $ sudo dpkg -i zenith_0.12.0-1_amd64.deb


* 启动

.. prompt:: bash $,# auto

   $ zenith


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210904004618016.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210904004618016.png
   :alt: image-20210904004618016


.. note:: 该可执行文件/命令行能快速提供有价值的信息


管理硬件
--------

v4l2
^^^^

v4l2设备支持vlc media player打开


* 安装

.. prompt:: bash $,# auto

   $ sudo apt install v4l-utils


* 查看相机所有属性

.. prompt:: bash $,# auto

   # v4l2-ctl -d <设备名> -all
   $ v4l2-ctl -d /dev/video0 --all

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/3XpxjcSwtiaE2DHP.jpg!thumbnail" alt="img" style="zoom: 67%; " />`


* 查看相机支持的像素格式

.. prompt:: bash $,# auto

   # v4l2-ctl --list-formats -d <设备名>
   $ v4l2-ctl --list-formats -d /dev/video0

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/HBOuewxlOL2nODH3.jpg!thumbnail" alt="img" style="zoom: 33%; " />`

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/WHtCs1tGSJbLycNu.jpg!thumbnail" alt="img" style="zoom: 33%; " />`


* 查看相机支持的分辨率和帧率

.. prompt:: bash $,# auto

   # v4l2-ctl --list-formats-ext -d <设备名>
   $ v4l2-ctl --list-formats-ext -d /dev/video2


* `手写yuyv转yuv420 <http://blog.mchook.cn/2018/03/07/YUYV(YUV422)%20to%20YUV420P/>`_

vlc media player
~~~~~~~~~~~~~~~~

无法显示USB相机的视频流时可尝试配置高级模式


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211110105514078.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211110105514078.png
   :alt: image-20211110105514078


监控设备温度
^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ sudo apt install lm-sensors
   $ watch -n 2 sensors

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/IY7gtxIT4cnCmLb0.png!thumbnail" alt="img" style="zoom:67%; " />`

查看设备信息
^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ lspci   # pci接口设备信息
   $ lsusb   # usb设备信息
   $ lshw -c <device_name>  # ls hardware


* lshw\ `可查询的设备 <https://ezix.org/project/wiki/HardwareLiSter>`_\ ：


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/vT62MX2KMPNm9DcH.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/vT62MX2KMPNm9DcH.png!thumbnail
   :alt: img



* 显卡信息显示不完全


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/UX2Bxt3z3hB4vskl.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/UX2Bxt3z3hB4vskl.png!thumbnail
   :alt: img


.. prompt:: bash $,# auto

   # 可先更新数据库
   $ sudo update-pciids

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/sV507p45ylC7xEa6.png!thumbnail" alt="img" style="zoom:67%; " />`

蓝牙
^^^^

hcitool
~~~~~~~


* 查看当前蓝牙设备

.. prompt:: bash $,# auto

   $ hcitool dev
   # Devices:
   #   hci0 30:E3:7A:1C:FE:E3


* 配置蓝牙连接

.. prompt:: bash $,# auto

   # 打开设备
   $ sudo hciconfig hci0 up
   # 关闭设备
   $ sudo hciconfig hci0 down
   # 查看附近的蓝牙设备
   $ sudo hcitool lescan
   # 连接某个蓝牙设备
   $ sudo hcitool cc <mac address>

rfkill
~~~~~~

用于管理无线设备（tool for enabling and disabling wireless devices）

.. prompt:: bash $,# auto

   $ rfkill

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211102120504265.png" alt="image-20211102120504265" style="zoom:50%;" />`

bluetoothctl
~~~~~~~~~~~~

.. prompt:: bash $,# auto

   $ bluetoothctl
   # 显示已配对的蓝牙
   $ paired-devices
   # 移除相关的配对 
   $ remove <mac_address>
   # 查看/关闭查看附近的蓝牙设备
   $ scan on/off
   # 进行配对
   $ connect <mac_address>

显卡
^^^^

`安装显卡驱动 <https://natsu-akatsuki.readthedocs.io/en/latest/ubuntu%E7%AC%94%E8%AE%B0/rst/%E7%A1%AC%E4%BB%B6%E4%B8%8E%E5%86%85%E6%A0%B8%E7%AE%A1%E7%90%86.html#id25>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`限制显卡功率 <https://blog.csdn.net/zjc910997316/article/details/113867906>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. prompt:: bash $,# auto

   # --persistence-mode= Set persistence mode: 0/DISABLED, 1/ENABLED
   $ sudo nvidia-smi -pm 1
   # --power-limit= Specifies maximum power management limit in watts.
   $ sudo nvidia-smi -pl 150

显示温度
~~~~~~~~

.. prompt:: bash $,# auto

   $ nvidia-smi --query-gpu=temperature.gpu --format=csv


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211101163639065.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211101163639065.png
   :alt: image-20211101163639065


内存
^^^^

清除内存缓存
~~~~~~~~~~~~

.. prompt:: bash $,# auto

   # 可先将内存数据写入到硬盘中，再清缓存
   $ sync 
   $ sudo bash -c "echo 3 > /proc/sys/vm/drop_caches"

清理swap
~~~~~~~~

.. prompt:: bash $,# auto

   # 直接清除（需内存有足够的空间来处理swap的数据）
   $ sudo swapoff -a; sudo swapon -a

`查看使用交换空间的进程 <https://www.cyberciti.biz/faq/linux-which-process-is-using-swap/>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. prompt:: bash $,# auto

   $ for file in /proc/*/status ; do awk '/VmSwap|Name/{printf $2 " " $3}END{ print ""}' $file; done | sort -k 2 -n -r

CPU
^^^

更改CPU工作模式
~~~~~~~~~~~~~~~

.. prompt:: bash $,# auto

   # 安装cpufrequtils
   $ sudo apt install cpufrequtils
   # 设置CPU工作模式
   $ cpufreq-set -g performance
   # 查看本机CPU支持的模式：                 
   $ sudo cpufreq-info

压力测试
~~~~~~~~

相关工具为stress, s-tui

.. prompt:: bash $,# auto

   $ sudo apt install s-tui stress

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210907110949467.png" alt="image-20210907110949467"  />`

实战
~~~~


* 温度过高。可通过 ``dmesg`` 或 ``journalctl`` 查看日志信息（日志等级不一定为err）

..

   mce: CPUx: Package temperature above threshold, cpu clock throttled


硬盘
^^^^


* 文件系统的类型： ``xfs`` 、 ``ext4`` ...
* 分区是硬盘的一个存储划分单元，一个硬盘由多个分区组成
* 分区被格式化，得到特定格式的文件系统后，才能正常使用/被读写
* 传统应用中，一个 ``分区`` 对应一个 ``文件系统``  

查看磁盘相关信息
~~~~~~~~~~~~~~~~


* 查看\ **文件系统**\ 的磁盘利用率

.. prompt:: bash $,# auto

   # -h: human-readable 以可读性强的方式显示
   $ df -h


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/GeX9NmnvmOdzae1i.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/GeX9NmnvmOdzae1i.png!thumbnail
   :alt: img



* 显示文件系统类型


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/apYZa6QKOpc4bVgb.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/apYZa6QKOpc4bVgb.png!thumbnail
   :alt: img



* 获取存储设备信息

.. prompt:: bash $,# auto

   $ lsblk # ls block device


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/WoOiWboFRizuIfKU.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/WoOiWboFRizuIfKU.png!thumbnail
   :alt: img


查看linux支持的文件系统
~~~~~~~~~~~~~~~~~~~~~~~


* 查看当前linux支持的文件系统

.. prompt:: bash $,# auto

   $ ls -l /lib/modules/$(uname -r)/kernel/fs


* 查看系统目前已加载到内存中支持的文件系统

.. prompt:: bash $,# auto

   $ cat /proc/filesystem

获取存储设备的分区表类型
~~~~~~~~~~~~~~~~~~~~~~~~

.. prompt:: bash $,# auto

   $ sudo parted device_name print


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/2GU2spATNM6x1CSm.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/2GU2spATNM6x1CSm.png!thumbnail
   :alt: img


.. note:: dpt对应gdisk命令；mbr对应fdisk命令


图形化分区工具
~~~~~~~~~~~~~~


* KDE partition manager (for kde)


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SGxhQJ8Uq5JJG4Xo.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SGxhQJ8Uq5JJG4Xo.png!thumbnail
   :alt: img


.. attention:: 修改完后记得apply


挂载
~~~~


* 命令行实现U盘挂载

.. prompt:: bash $,# auto

   # 查看设备名 p: (paths) print full device paths 
   $ lsblk -p
   $ mount <device_name> <mount_point>

.. note:: 挂载点需已创建(mkdir)



* 无法粘贴数据到挂载盘

情况一：挂载盘或为只读属性，需修改读写属性和重新挂载

.. prompt:: bash $,# auto

   $ sudo mount -o remount rw <挂载点>
   # -o: option
   # --bind： mount --bind <olddir> <newdir> 重新挂载

情况二：文件名不兼容(for windows)

例如linux允许文件名带 ``:`` ，win不允许带 ``:`` ，因此不能进行粘贴操作


* 
  `开机自启动挂载 <https://blog.csdn.net/okhymok/article/details/76616892>`_

  修改 ``/etc/fstab`` 配置文档，详细说明可看使用文档 ``man fstab``\ ，查看UUID和type可使用命令行

.. prompt:: bash $,# auto

   $ sudo blkid


* `从windows访问linux的ext4文件系统 <https://www.diskinternals.com/linux-reader/access-ext4-from-windows/>`_

windows默认不支持ext4文件系统的读写，需要下载软件实现额外的支持


* U盘格式化（for KDE）：Disks


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220104145417626.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220104145417626.png
   :alt: image-20220104145417626


`输入设备 <https://wiki.archlinux.org/title/Xorg>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   # 显示输入设备 
   $ xinput 
   # 禁用/启动某个输入设备 
   $ xinput enable/disable <device_id>


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/qRGjseKCAT2Tlq66.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/qRGjseKCAT2Tlq66.png!thumbnail
   :alt: img


USB
^^^


* 查看设备的usb版本号（2.0 or 3.0）


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211203140239039.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211203140239039.png
   :alt: image-20211203140239039


.. note:: 从外部看，四引脚为2.0，九引脚为USB3.0



* `USB 功率 <https://en.wikipedia.org/wiki/USB#Power>`_


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211203141044757.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211203141044757.png
   :alt: image-20211203141044757



* USB口示意图


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/v2-f3430ba5c29d68a8a2f07d040b9be449_r.jpg
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/v2-f3430ba5c29d68a8a2f07d040b9be449_r.jpg
   :alt: preview


`外设绑定 <https://wiki.archlinux.org/title/Udev>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

基于计算机设备端口号的绑定固定名称
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

步骤一：查看当前串口

.. prompt:: bash $,# auto

   $ ls /dev/ttyUSB*

步骤二：查看串口详细信息

.. prompt:: bash $,# auto

   $ udevadm info /dev/ttyUSB*


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/Sz8pWieZ3CVLihbE.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/Sz8pWieZ3CVLihbE.png!thumbnail
   :alt: img


.. note:: 图中红框处为端口对应的硬件上的USB口 ID


步骤三：创建文件

.. prompt:: bash $,# auto

   $ cat /etc/udev/rules.d/com_port.rules

步骤四：添加内容

.. prompt:: bash $,# auto

   ACTION=="add",KERNELS=="{ID}",SUBSYSTEMS=="usb",MODE:="0777",SYMLINK+="{name}"

.. note:: 其中{ID}为红框处的USB口ID，{name}为该端口别名


`udev配置语法 <https://blog.csdn.net/xiaoliu5396/article/details/46531893?locationNum=2>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

实战：相机端口绑定(/dev/video*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

步骤一：看属性

.. prompt:: bash $,# auto

   # 查看硬件设备生厂商和销售商id
   $ dmesg 
   # 或 
   $ udevadm info -a <设备挂载点> | grep id


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/Sbk14kPkgUQz5qIm.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/Sbk14kPkgUQz5qIm.png!thumbnail
   :alt: img



.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/ORJOpxs27Z2j2JHf.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/ORJOpxs27Z2j2JHf.png!thumbnail
   :alt: img


步骤二：构建规则文档

.. prompt:: bash $,# auto

   KERNELS=="video*",  ATTRS{idVendor}=="2a0b", ATTRS{idProduct}=="00db", MODE:="0666", SYMLINK+="camera0"

内核
----

apt安装
^^^^^^^

.. prompt:: bash $,# auto

   $ version="5.11.0-44"
   $ sudo apt install linux-image-${version}-generic linux-headers-${version}-generic linux-modules-${version}-generic linux-modules-extra-${version}-generic

.. note:: 遗漏module模块或无法识别wifi/声卡模块


查看已安装的内核版本
^^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ dpkg --get-selections | grep linux-image

升级内核以解决硬件驱动无法识别的问题
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


* `通过官方源升级内核（bash脚本） <https://github.com/pimlie/ubuntu-mainline-kernel.sh>`_

非ubuntu21版本，从官方源下载最新内核或有问题（官方源的内核编译时依赖21的库）


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/BL2DG8orSBiQroYp.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/BL2DG8orSBiQroYp.png!thumbnail
   :alt: img



* 在ubuntu20.04上升级内核到5.10+(ppa)

`可使用20.04的库编译的内核（能用，但内核会有err日志） <https://launchpad.net/~tuxinvader/+archive/ubuntu/lts-mainline>`_

.. prompt:: bash $,# auto

   $ sudo add-apt-repository ppa:tuxinvader/lts-mainline
   $ sudo apt-get update
   # e.g. install v5.12
   $ sudo apt-get install linux-generic-5.12


* (recommend)在ubuntu20.04升级到5.10+(oem)，\ `HWE <https://ubuntu.com/kernel/lifecycle>`_

.. prompt:: bash $,# auto

   $ apt install linux-oem-20.04b

   # 2022.3.23: 5.13
   $ sudo apt-get install --install-recommends linux-generic-hwe-20.04

拓展资料
~~~~~~~~


* 
  `processors' generation codename <https://www.intel.com/content/www/us/en/design/products-and-solutions/processors-and-chipsets/platform-codenames.html>`_

* 
  `a discussion for Nvidia GPU <https://forums.developer.nvidia.com/t/ubuntu-mate-20-04-with-rtx-3070-on-ryzen-5900-black-screen-after-boot/167681>`_

原地升级ubuntu版本
^^^^^^^^^^^^^^^^^^

若当前系统没有重要的文件、应用程序保留，建议直接镜像+U盘从头安装，避免还要解决依赖问题，以下以18.04升级到20.04为例，描述涉及的解决方案。未尽事宜，看输出的日志信息而进行针对性的解决。另外原地升级需要较长的时间，若时间紧迫，建议直接重装。升级完后，有些第三方应用程序或驱动(application or driver )可能需要进行重装或升级。例如，重装显卡驱动。


* 步骤一：删包

.. prompt:: bash $,# auto

   # 有ros时需卸载18版本的ros
   $ sudo apt purge --autoremove ros-melodic-*


* 步骤二：删源

删除18用到的第三方源（否则升级系统而升级安装包时，会使用到18的第三方源，例如ppa），最佳实践是只保留ubuntu官方的仓库软件源

.. prompt:: bash $,# auto

   $ sudo rm -rf /etc/apt/sources.list.d


* 步骤三：升级系统

.. prompt:: bash $,# auto

   $ sudo apt update
   $ sudo apt upgrade
   $ sudo do-release-upgrade

.. note:: 若 ``do-release-upgrade`` 没找到可用的发行版，可以看看是不是 ``/etc/update-manager/release-upgrades`` 中禁用了更新；用这种方法若从16.04升级到20.04需要经过两次升级(16.04->18.04->20.04)


拓展资料
~~~~~~~~


* `ubuntu version history <https://ubuntu.com/about/release-cycle>`_\ ，\ `维基 <https://en.wikipedia.org/wiki/Ubuntu_version_history#Table_of_versions>`_\ 的有点老，还是得看一波官网的

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211101161245968.png" alt="image-20211101161245968"  />`

内核模块
^^^^^^^^


* ``.ko``\ 内核模块后缀，一般位于\ ``/lib/moudles/$(uname -r)/kernel``\ 下

常用指令
~~~~~~~~

.. prompt:: bash $,# auto

   $ lsmod       # 查看已加载的内核模块（可显示某个模块被调用的情况）
   $ modinfo <module_name>      # 查看内核模块（包括.ko文件）的描述信息
   $ modprobe <module_name>     # 加载内核模块（自动解决依赖问题）
   $ modprobe -r <module_name>  # unload内核模块（自动解决依赖问题）

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/1aanmMC4HTegOW8H.png!thumbnail" alt="img" style="zoom:50%;" />`

设置模块自启动
~~~~~~~~~~~~~~

将相关模块放置于配置文档 ``/etc/modules``

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/P06oQFeLsuYRmDeI.png!thumbnail" alt="img" style="zoom:50%;" />`

拓展资料
~~~~~~~~


* `load/unload内核 <https://opensource.com/article/18/5/how-load-or-unload-linux-kernel-module>`_

限制用户使用资源(optional)
--------------------------

显示当前的限制状态
^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ ulimit -a

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/TWAvA2t4Oy0sLJpw.png!thumbnail" alt="img" style="zoom:50%;" />`

`修改用户ext磁盘资源 <https://wiki.archlinux.org/title/Disk_quota>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

步骤一：修改配置文件 ``/etc/security/limits.conf`` ，并重新挂载


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/ExBExP9VsNcTAXy3.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/ExBExP9VsNcTAXy3.png!thumbnail
   :alt: img


步骤二：创建quoto index

.. prompt:: bash $,# auto

   $ quotacheck -cum <相关路径>
   $ quotaon -v <相关路径>

步骤三：限制用户配额（交互式）

.. prompt:: bash $,# auto

   $ edquota <user_name>

`使用chroot修复系统 <https://help.ubuntu.com/community/LiveCdRecovery>`_
----------------------------------------------------------------------------


* chroot的作用相当于在系统B（引导盘）执行系统A（受损系统）的可执行文件，以下为使用chroot来修复镜像

.. prompt:: bash $,# auto

   # 挂载系统盘
   # mount <device_name> <mount_point>
   $ sudo mount /dev/sda1 /mnt
   $ sudo mount --bind /dev /mnt/dev
   $ sudo mount --bind /proc /mnt/proc
   $ sudo mount --bind /sys /mnt/sys
   $ sudo mount <boot位置> /mnt/boot
   # 切换根目录
   $ sudo chroot /mnt

   # todo ...

   # 取消挂载
   $ umount /mnt/boot
   $ umount /mnt/sys
   $ umount /mnt/proc
   $ umount /mnt/dev
   $ umount /mnt/


* `其他应用 <https://help.ubuntu.com/community/LiveCdRecovery>`_\ （已尝试过可修改分区）
