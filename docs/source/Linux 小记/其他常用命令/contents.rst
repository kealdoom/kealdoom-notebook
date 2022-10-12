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