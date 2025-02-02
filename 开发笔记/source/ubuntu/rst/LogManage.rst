.. role:: raw-html-m2r(raw)
   :format: html


LogManage
=========

查看内核日志
------------

dmesg
^^^^^

可用于查看内核自检信息（e.g. 硬件的检测流程）；判断外设是否成功连接

.. prompt:: bash $,# auto

   $ dmesg
   # option:
   # -l (level) 设置输出等级
   # -T (timestamp) 使用系统时间（时间或在挂起后不准）

----

**可用等级**

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/vOHQFX5VXsRvIUZ8.png!thumbnail" alt="img" style="zoom:67%;" />`

**有关时间的补充说明**


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SoEqKDAjyTkGHhsQ.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SoEqKDAjyTkGHhsQ.png!thumbnail
   :alt: img


----

解决方案
~~~~~~~~


* `启动项加入新的选项 <https://bbs.archlinux.org/viewtopic.php?id=246507>`_


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/B8YXQPNwb5apZQ7A.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/B8YXQPNwb5apZQ7A.png!thumbnail
   :alt: img


journalctl
^^^^^^^^^^

详看 :ref:`查看服务日志`

查看用户日志
------------

含访问记录(login/logout)、登录验证信息(authority)

查看服务日志
------------

journalctl
^^^^^^^^^^

.. prompt:: bash $,# auto

   $ journalctl -x # 输出信息附帮助性说明(help texts)
   $ journalctl -e # 指定从日志文件尾部读起


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SM3t7ubZHhPqIQAR.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/SM3t7ubZHhPqIQAR.png!thumbnail
   :alt: img


限制性输出
~~~~~~~~~~

.. prompt:: bash $,# auto

   # option
   # -p: err/num      # 指定日志输出等级
   # --: since today  # 指定起始日期（只看当天的日志）
   # -b：             # 最近一次的boot记录
   # -k：             # 只查看内核信息


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/cmfj6YFCuKa3q2dr.png!thumbnail
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/cmfj6YFCuKa3q2dr.png!thumbnail
   :alt: img


拓展：\ `一般使用journalctl来读取内核日志，而不用dmesg <https://wiki.archlinux.org/title/General_troubleshooting#General_procedures>`_

查看日志占用的磁盘空间
~~~~~~~~~~~~~~~~~~~~~~

.. prompt:: bash $,# auto

   $ journalctl --disk-usage

查看所有日志
------------

即可通过GUI查看内核、用户、服务等日志

for KDE
^^^^^^^

.. prompt:: bash $,# auto

   $ ksystemlog

:raw-html-m2r:`<img src="https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/7ThlxRbwntAjiso8.png!thumbnail" alt="img" style="zoom:80%;" />`

`lnav <http://www.imooc.com/article/80502>`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

具有文本高亮，突出重点的效果


.. image:: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211030104458267.png
   :target: https://natsu-akatsuki.oss-cn-guangzhou.aliyuncs.com/img/image-20211030104458267.png
   :alt: image-20211030104458267


日志DEBUG
---------

PKCS#7 signature not signed with a trusted key
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

显卡驱动异常，重装显卡驱动
