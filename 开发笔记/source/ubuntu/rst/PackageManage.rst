.. role:: raw-html-m2r(raw)
   :format: html


PackageManage
=============

apt && dpkg
-----------

常用命令行
^^^^^^^^^^

.. prompt:: bash $,# auto

   $ apt clean                 # 清除安装包
   $ apt remove <pkg_name>  # 卸载软件，保留配置文件
   $ apt purge <pkg_name>   # 卸载软件和相关的配置文件
   $ apt autoremove            # 卸载已无用和自动安装的软件
   $ apt dist-upgrade     # 升级安装包（升级时会删除一些影响依赖的包）
   $ apt-mark hold <pkg_name> # 将某些包设置为手动更新

   $ dpkg -i <deb_package>     # 安装包
   # -r: remove
   # -P: purge（此处为大写）
   # 也可以使用gdebi（需安装），其能更好的解决依赖问题
   $ gdebi <deb_package>  # 安装

.. note:: apt比apt-get具有更高层的封装



.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/R4zpxUhoGXPLpgN0.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/R4zpxUhoGXPLpgN0.png!thumbnail
   :alt: img


.. hint::  dist-upgrade适用于"The following packages have been kept back"的情况


查看apt包的依赖信息
^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   # 除了显示依赖信息还会显示package的其他信息（如maintainer,recommends packages）
   $ apt show <package_name>
   # 仅显示依赖信息
   $ apt-cache depends <package_name>

显示deb包的依赖信息
^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   # Show information about a package
   $ dpkg -I <archive/deb>

显示apt包的依赖链(apt dependency chain)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ sudo apt install apt-rdepends
   $ apt-rdepends -p <package_name>
   # -p: 在依赖包后面追加状态信息
   # -r：显示哪些package依赖当前的package

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210906141516268.png" alt="image-20210906141516268" style="zoom:67%; " />`

----

**NOTE**

要显示哪些包未安装，虽然该命令行有option可配置，但是使用上感觉如下命令行更方便

.. prompt:: bash $,# auto

   $ apt-rdepends -p <package_name> | grep NotInstalled

----

显示已安装的包
^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ apt list --install
   $ dpkg -l

删除无用的配置文档
^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   $ dpkg -l | grep "^rc" | awk '{print $2}' | sudo xargs apt -y purge

`增删PPA仓库 <https://linuxconfig.org/how-to-list-and-remove-ppa-repository-on-ubuntu-18-04-bionic-beaver-linux>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DEBUG
^^^^^

updates for this repository will not be applied
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

使用apt更新源时会出现如上报错，或同步下系统时间即可

pip
---

常用命令行
^^^^^^^^^^

.. prompt:: bash $,# auto

   # ---下载--- #
   $ pip install --upgrade / -U <pkg_name>  # 升级给定package
   $ pip install -r <requirements.txt>      # 下载文档中给定的依赖
   $ pip install -i <某源>                  # 通过给定源进行下载
   $ pip install --no-cache-dir             # 不保留缓存地安装
   # ---查看包信息--- #
   $ pip show <pkg_name>
   $ pip list --outdate     # 查看可升级的包
   # ---pip安装到当前用户--- #
   $ pip install --user <pkg_name>
   # ---清除pip缓存--- #
   $ rm -r ~/.cache/pip
   # ---卸载包及其依赖--- #
   # pip install pip-autoremove
   $ pip-autoremove <pkg

.. attention:: pip没有一键升级所有安装包的命令行，感觉是因为他不能够解决python包的依赖问题


wget
----

.. prompt:: bash $,# auto

   $ wget -c <链接> -O <file_name>
   # -c: 断点下载
   # -O：重命名

.. hint:: aria2据说为增强版wget


curl
----

.. prompt:: bash $,# auto

   $ curl
   # -k, --insecure      Allow insecure server connections when using SSL
   # -i, --include       Include protocol response headers in the output
   # -s, --silent        Silent mode
   # -L, --location      Follow redirects (配合tee重定向输出数据到文件)
   # --output <file>     Write to file instead of stdout


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211101171306726.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211101171306726.png
   :alt: image-20211101171306726


snap
----

unix-like自带，安装的应用程序有点像docker容器，整体体积会较大

常用命令行
^^^^^^^^^^

.. prompt:: bash $,# auto

   $ snap list                           # 列出已安装的snap包
   $ sudo snap remove <pkg>              # 卸载snap中安装的包
   $ sudo apt autoremove --purge snapd   # 卸载snap-core

conda
-----

安装
^^^^

步骤一：\ `下载安装包 <https://www.anaconda.com/products/individual>`_

.. prompt:: bash $,# auto

   $ wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh -O ./anaconda.sh
   $ conda update conda

步骤二：交互模式执行安装包（此方法可顺带初始化conda）

----

**NOTE**\ ：无交互式的安装

.. prompt:: bash $,# auto

   $ /bin/bash anaconda.sh -b -p /opt/conda 
   $ 'export PATH=/opt/conda/bin:$PATH' >> ~/.bashrc 
   $ conda init 
   $ conda config --set auto_activate_base false $
   $ conda update conda

   # -b run install in batch mode (without manual intervention), it is expected the license terms are agreed upon
   # -p PREFIX  install prefix, defaults to $PREFIX, must not contain spaces.

----

配置文档
^^^^^^^^


* 默认不启动conda环境

.. prompt:: bash $,# auto

   $ conda config --set auto_activate_base false

查询信息
^^^^^^^^


* 查询当前环境的所有packages的相关信息

.. prompt:: bash $,# auto

   $ conda list
   # -n <env>: 指定环境


* 查询当前已安装的conda环境

.. prompt:: bash $,# auto

   $ conda env list


* 查询安装历史

.. prompt:: bash $,# auto

   $ conda list --revisions

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/I1JHF95b6IDEWj7M.png!thumbnail" alt="img" style="zoom:67%; " />`


* 查询conda应用程序的相关信息

.. prompt:: bash $,# auto

   $ conda info

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20210906223711162.png" alt="image-20210906223711162" style="zoom: 50%; " />`

安装和更新包
^^^^^^^^^^^^

.. prompt:: bash $,# auto

   # 根据文件更新当前环境
   $ conda env update -f <文件名>
   # 跳过interaction进行安装
   $ conda install -y
   # 包的导出和导入
   $ conda env export -n 环境名 > 文件名.yml
   $ conda env create -f 文件名.yml

----

**NOTE**

文件解析：

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/XAWWBAeAbYBXrJRM.png!thumbnail" alt="img" style="zoom:67%; " />`

----

升级conda
^^^^^^^^^

.. prompt:: bash $,# auto

   $ conda update conda

清理
^^^^

.. prompt:: bash $,# auto

   # 删除缓存、索引等
   $ conda clean -a
   # 删除环境
   $ conda env remove -n <env_name>
   # 删除包
   $ conda remove -n <env_name> <pkg>

.. note:: 注意conda使用的是remove而不是install（该命令能够根据依赖关系删包）


触发命令行补全
^^^^^^^^^^^^^^

conda并不提供内部补全的插件，需要\ `安装第三方插件 <https://github.com/tartansandal/conda-bash-completion>`_

步骤一：安装

.. prompt:: bash $,# auto

   $ conda install -n base -c conda-forge conda-bash-completion

步骤二：添加到~/.bashrc

.. prompt:: bash $,# auto

   # 配置conda代码补全
   CONDA_ROOT="${HOME}/anaconda3"
   if [[ -r $CONDA_ROOT/etc/profile.d/bash_completion.sh ]]; then
       source $CONDA_ROOT/etc/profile.d/bash_completion.sh
   fi

.. attention:: 记得修改对应的目录


环境复制
^^^^^^^^


* 本地环境的复制

.. prompt:: bash $,# auto

   $ conda create --clone <被复制的环境> -n <粘贴的环境名>

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/jOxAQgSIQCmervG3.png!thumbnail" alt="img" style="zoom:67%; " />`


* `同操作环境下环境的迁移或部署 <https://conda.github.io/conda-pack/>`_\ （\ `中文翻译 <https://zhuanlan.zhihu.com/p/87344422>`_\ ）

.. prompt:: bash $,# auto

   # base环境下安装 
   $ conda install conda-pack 
   # src机上打包指定环境 
   $ conda pack -n <环境名> 
   # dst机上解压缩（tar...），解压缩到env目录下 
   $ ... 
   # 修复python package前缀项(conda-unpack在bin目录下) 
   $ conda activate <环境名>  && conda-unpack

.. hint:: 虽然conda pack最终的效果是生成一个压缩包，但跟自己用tar生成的压缩包不同，其还在压缩时添加了一些用于解决导出的python包路径错误问 的脚本，如conda-unpack。


实战
^^^^

多线程提高下载速度
~~~~~~~~~~~~~~~~~~

用\ `mamba <https://github.com/mamba-org/mamba>`_\ 来安装包

.. prompt:: bash $,# auto

   $ conda install -n base -c conda-forge mamba
   $ mamba install <package_name>

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/CP0aVRAsWIAQWpl3.png!thumbnail" alt="img" style="zoom:50%; " />`

`多用户下conda的配置 <https://docs.anaconda.com/anaconda/install/multi-user/>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

拓展资料
^^^^^^^^


* `conda 说明文档 <https://docs.conda.io/projects/conda/en/latest/user-guide/>`_
* `参数配置文档1 <https://conda.io/projects/conda/en/latest/user-guide/configuration/index.html>`_\ 、\ `参数配置文档2 <https://conda.io/projects/conda/en/latest/configuration.html?highlight=custom_channels%3A>`_
* `任务导向说明 <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html>`_
* `conda-vs-pip-vs-virtualenv-commands <https://docs.conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands>`_

`PPA <https://launchpad.net/ubuntu/+ppas>`_
-----------------------------------------------

`添加PPA到PC <https://help.launchpad.net/Packaging/PPA/InstallingSoftware>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. prompt:: bash $,# auto

   # sudo add-apt-repository ppa:user/ppa-name
   $ sudo add-apt-repository ppa:natsu-akatsuki/sleipnir

.. note:: 本质上是往 ``/etc/apt/sources.list.d`` 中添加source.list


`创建PPA <https://help.launchpad.net/Packaging/PPA>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Activating a PPA

打包一个文件到PPA
^^^^^^^^^^^^^^^^^

步骤一：\ `上传GPG到ubuntu server <https://help.ubuntu.com/community/GnuPrivacyGuardHowto>`_\ ，以让所有客户端可获取

.. prompt:: bash $,# auto

   # gpg --keyserver keyserver.ubuntu.com --send-keys <yourkeyID>
   $ gpg --keyserver keyserver.ubuntu.com --send-keys 96037357E6D61138
   # 查看是否上传成功
   $ gpg --keyserver hkp://keyserver.ubuntu.com --search-key <yourkeyID>

步骤二：\ `launchpad中添加GPG密钥 <https://launchpad.net/+help-registry/import-pgp-key.html>`_


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220125003446149.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220125003446149.png
   :alt: image-20220125003446149


步骤三：生成template

.. prompt:: bash $,# auto

   # cd到待打包的文件中
   $ dh_make --createorig -s -y
   $ dh_make -p tutorial_0.0.1 --single --native --copyright mit --email hong877381@gmail.com
   # optioin:
   # -y, --yes             automatic yes to prompts and run non-interactively
   # -s, --single          set package class to single
   # -i, --indep           set package class to arch-independent
   # -l, --library         set package class to library
   # --python              set package class to python
   # --createorig
   $ rm debian/*.ex debian/*.EX   # 删除不需要的文件

.. note:: For dh_make to find the package name and version, the current directory needs to be in the format of <package>-<version>. Alternatively use the_-p flag using the format <name>_<version> to override it. The directory name you have specified is invalid!



* 其中主要是要完善changelog、copyright、control文件

----

**ATTENTION**


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220125105404202.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20220125105404202.png
   :alt: image-20220125105404202


----

.. prompt:: bash $,# auto

   $ perl -i -0777 -pe "s/(Copyright: ).+\n +.+/\${1}$(date +%Y) natsu-akatsiku Foo <hong877381@gmail.com>/" copyright

步骤四：构建deb包


* 填写完成后即进行打包和sign

.. prompt:: bash $,# auto

   $ sudo apt-get install devscripts build-essential lintian
   # 等价于：cd到待打包的目录，构建deb包
   $ dpkg-buildpackage -us -uc
   # option:
   # -us, --unsigned-source      unsigned source package
   # -uc, --unsigned-changes     unsigned .buildinfo and .changes file.

   # sign .changes file（会同时把dsc, buildinfo也sign了）
   $ debsign -k <keyID> <filename>.changes

   # 要一体化dpkg-buildpackage和debsign命令则可以使用debuild命令
   # 打包和sign文件，注意k后无空格
   $ debuild -k<keyID> -S

步骤五：\ `上传文件到PPA <https://help.launchpad.net/Packaging/PPA/Uploading>`_

.. prompt:: bash $,# auto

   $ sudo apt install dput
   # dput ppa:your-lp-id/ppa <source.changes>
   $ dput ppa:natsu-akatsuki/sleipnir <source.changes>

.. note:: 可查看绑定邮件看上传情况


Q&A
~~~


* Failed to add key. helios@helios:\ **~**\ $ sudo add-apt-repository ppa:natsu-akatsuki/sleipnir. More info: https://launchpad.net/~natsu-akatsuki/+archive/ubuntu/sleipnir. Press [ENTER] to continue or Ctrl-c to cancel adding it. Error: signing key fingerprint does not exist. Failed to add key.

..

   等一段时间。（已设置GPG的情况下）package上传成功后，不会很快生效，需要等一段时间。



* `上传失败 <https://help.launchpad.net/Packaging/UploadErrors>`_

参考资料
^^^^^^^^


* `ppa-guide之十万个为什么 <https://itsfoss.com/ppa-guide/>`_
* `利用debuild整合版工具来构建deb包 <https://blog.packagecloud.io/buildling-debian-packages-with-debuild/>`_
* `debian目录的相关描述 <https://packaging.ubuntu.com/html/debian-dir-overview.html>`_

关闭gnome的软件更新自启动
-------------------------

.. prompt:: bash $,# auto

   $ sudo rm /etc/xdg/autostart/update-notifier.desktop
