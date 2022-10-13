其他常用命令
===================

find
-------------------

find是linux中常用的查找工具，其基础命令格式：

.. code-block:: sh

    find path

该命令会遍历打印出指定目录下的所有目录及文件。

find命令支持基于通配符、正则表达式、目录树深度、文件日期和文件类型等条件查找文件。

- 通过文件名或正则表达式进行查找：

.. code-block:: sh

    find . -name '*.c'

    find . -path '*/test/*' -name '*.c'

    #还支持逻辑操作符or和and
    find . \( -name '*.txt' -o -name '*.pdf' \)
    find . \( -name '*.txt' -a -name '*.pdf' \)

    # -regex选项基于正则表达式进匹配
    find . -regex '.*\.\(py\|sh\)$'

- 通过 ``!`` 排除匹配到的模式：

.. code-block:: sh

    find . ! -name '*.c'

- 限定find命令遍历的目录深度：

.. code-block:: sh

    find . -maxdepth 5 -name '*.c'

    find . -mindepth 2 -name '*.c'

- 根据文件类型搜索：

.. code-block:: sh

    find . -type f  #查找文件
    find . -type l  #查找链接
    find . -type d  #查找目录

- 根据文件的时间戳搜索：

.. code-block:: sh

    find . -type f -atime -7    #打印出在7天内被访问过的文件

    find . -type f -mtime +7    #打印出最后修改时间超过7天的文件

- 根据文件大小搜索：

.. code-block:: sh

    find . -type f -size +2k

    find . -type f -size +5G

- 根据文件权限和所有权搜索：

.. code-block:: sh

    find . -perm 600

    find . -user root

- 利用find执行操作：

删除匹配文件:

.. code-block:: sh

    find . -name '*.c' -delete

执行命令：

.. code-block:: sh

    find . -type f -name '*.c' -exec cat {} > all_c_file.txt \;

xargs命令
--------------------------

- xargs一般紧跟在管道符之后，重新格式化stdin接收到的数据，再将其作为参数提供给指定命令，如：

.. code-block:: sh

    ls *.c | xargs grep main

- xargs可以使用 ``-n`` 选项指定每次调用命令时用到的参数个数，使用 ``-d`` 选项自定义分隔符：

.. code-block:: sh

    $echo "splitXsplitXsplitXsplitX" | xargs -d X -n 2
        split split
        split split

- 默认情况下，xargs命令会把参数放置在指定命令的尾部，而使用 ``-I`` 选项可以用于指定替换字符串，以此也可以为多组命令提供参数：

.. code-block:: sh

    ls *.c | xargs -I {} cp {} tmp/

sort和uniq
------------------------------

sort命令的常用选项如下：

-d  按字典序排序
-n  按照数字顺序排序
-r  逆序排序
-k num  以第k列作为主元排序
-M  按月份排序
-m  合并两个已排序文件
-c  检查文件是否排序过

uniq只能作用于排序后的数据，报告或删除重复的行，因此通常和sort一同使用。

uniq命令的常用选项如下：

-u  只显示未重复行
-d  只显示重复行
-c  显示各行在文件中的出现次数
-z  生成由0值字节终止的输出，用于和xargs联用

%和#操作符切分文件名
-------------------------------

借助 ``%`` 操作符可以从name.extension这种格式中提取出name，借助 ``#`` 操作符可以提取出extension，具体用法如下：

::

    ${VAR%.*}

从VAR中删除位于 ``%`` 右侧的通配符所匹配的字符串，通配符从右向左以非贪婪模式匹配， ``%%`` 为贪婪模式。

::

    ${VAR#*.}

从VAR中删除位于 ``#`` 右侧的通配符所匹配的字符串，通配符从左向右以非贪婪模式匹配， ``##`` 为贪婪模式。

