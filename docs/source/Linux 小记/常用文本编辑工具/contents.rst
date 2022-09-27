常用文本编辑工具
=======================

gawk
------------

gawk 基础
+++++++++++++++++

gawk命令格式
~~~~~~~~~~~~~~~

gawk的基本命令格式如下：

**gawk** *option program file*

常用的gawk选项：

-F fs  指定行中划分数据字段的字段分隔符

从命令行中读取程序脚本
~~~~~~~~~~~~~~~~~~~~~~

运行gawk程序，需要将脚本命令放到两个花括号 ``{}`` 中。此外，由于gawk假定脚本是单个字符串，所以在使用多个字符串的脚本时，还需要将其放到单引号中。

下面是一个简单的gawk程序脚本：

.. code-block:: sh
    :linenos:

    $ gawk '{print "Hello world!"}'

数据字段变量
~~~~~~~~~~~~~~~~~~~~~

gawk会自动给一行中的每个数据元素分配一个变量，默认情况下，gawk按如下方式分配变量：

- $0代表整个文本行；
- $1代表文本行中的第一个数据段；
- $2代表文本行中的第二个数据段；
- $n代表文本行中的第n个数据段。

gawk在读取一行文本时，会用预定义的字段分隔符划分每个数据字段，默认的字段分隔符是任意的空白字符。

可以用 `-F` 选项指定分隔符, 也可以在脚本中使用 ``FS=`` 指定分隔符：

.. code-block:: sh

    $ gawk -F: '{print $1}' /etc/passwd
        root
        daemon
        bin
        sys
        sync
    $

    或者

    $ gawk '{FS=":"; print $1}' /etc/passwd

在程序脚本中使用多个命令
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

可以通过分号 `；` 将多条gawk命令组合成一个正常的程序。

.. code-block:: sh

    $ echo "Welcome to Kealdoom notebook" | gawk '{$3="Wtfzues"; print $0}'
        Welcome to Wtfzues notebook
    $

    或者

    $ gawk '{$3="Wtfzues"
    > print $0}'
    > Welcome to Kealdoom notebook
        Welcome to Wtfzues notebook
    $

在运行后一个示例时，需要使用Ctrl+D组合键产生EOF字符，表明输入结束。

在处理数据前后运行脚本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

默认情况下，gawk会从输入中读取一行文本，然后针对该行的数据执行脚本。通过添加 ``BEGIN`` 和 ``END`` 关键字可以强制gawk在读取数据前、后执行脚本。

只使用 ``BEGIN`` :

.. code-block:: sh

    $ cat file1
        line 1
        line 2
        line 3
    $
    $ gawk 'BEGIN {print "This is title"} {print $0}' file1
        This is title
        line 1
        line 2
        line 3
    $

联用 ``BEGIN`` 和 ``END`` :

.. code-block:: sh

    $ gawk 'BEGIN {print "This is title"}
    > {print $0}
    > END {print "This is end"}' file1
        This is title
        line 1
        line 2
        line 3
        This is end

gawk 进阶
+++++++++++++++

变量
~~~~~~~~~~~~~~~~

gawk 支持2种类型不同的变量：

- **内建变量**
- **自定义变量**

内建变量
***************

gawk 程序使用内建变量来引用程序数据中的特殊功能，首先介绍其中数据字段和记录相关的变量。

.. list-table:: gawk数据字段和记录变量
    :widths: 10 40
    :align: center
    :header-rows: 1

    * - 变量
      - 描述
    * - FIELGWIDTHS
      - 由空格分隔的一列数字，定义了每个数据字段确切宽度
    * - FS
      - 输入字段分隔符
    * - RS
      - 输入记录分隔符
    * - OFS
      - 输出字段分隔符
    * - ORS
      - 输出记录分隔符



