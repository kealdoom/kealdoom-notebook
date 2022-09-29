逻辑控制流
===================

本节主要记录shell脚本中的逻辑控制流语法以及可用的参数。

if语句
-------------------

if语句基本结构
~~~~~~~~~~~~~~~~~~~

shell中的if语句格式如下：

.. code-block:: sh

    if command1
    then
        commands
    elif command2
    then
        commands
    else
        commands
    fi

bash shell的if语句会立刻运行紧跟if之后的命令，如果该命令的退出状态码为0，就会执行then部分的命令。

if语句只接受退出状态码作为条件测试，因此在实际使用场景中往往需要借助test命令或者方括号通过测试。

如果test命令中列出的条件成立，该命令就会退出并返回退出状态码0，test命令格式如下：

.. code-block:: sh

    test condition

其中 ``condition`` 是test命令要测试的一系列参数和值，如果不提供 ``condition`` 语句，则会返回非0的退出状态码。

使用test命令的if语句格式如下：

.. code-block:: sh

    if test condition
    then
        commands
    fi

使用方括号的语法如下：

.. code-block:: sh

    if [ condition ]
    then
        commands
    fi

.. attention::
    第一个方括号之后和第二个方括号之前必须加上空格，否则会报错。

if测试条件
~~~~~~~~~~~~~~~~~~~

**数值比较：**

.. list-table:: 数值比较
    :widths: 15, 40
    :header-rows: 1

    * - 比较
      - 描述
    * - n1 -eq n2
      - 检查n1是否与n2相等
    * - n1 -ge n2
      - 检查n1是否大于或等于n2
    * - n1 -gt n2
      - 检查n1是否大于n2
    * - n1 -le n2
      - 检查n1是否小于或等于n2
    * - n1 -lt n2
      - 检查n1是否小于n2
    * - n1 -ne n2
      - 检查n1是否不等于n2

.. attention::
    bash shell只能处理整数，如果直接使用浮点数参与数据比较会报错。

**字符串比较：**

.. list-table:: 字符串比较
    :widths: 15, 40
    :header-rows: 1

    * - 比较
      - 描述
    * - str1 = str2
      - 检查str1是否和str2相同
    * - str1 != str2
      - 检查str1是否和str2不同
    * - str1 < str2
      - 检查str1是否小于str2
    * - str1 > str2
      - 检查str1是否大于str2
    * - -n str1
      - 检查str1的长度是否非0
    * - -z str1
      - 检查str1的长度是否为0

.. attention::
    在比较字符串大小时有2个常见错误：

    - shell默认会将大于号和小于号视为重定向符，同时把字符串视为文件名。因此，必须将大于号和小于号进行转义。
    - 比较测试根据标准的ASCII决定排序结果，数字 < 大写字母 < 小写字母。

**文件比较：**

.. list-table:: 文件比较
    :widths: 15, 40
    :header-rows: 1

    * - 比较
      - 描述
    * - -d file
      - 检查file是否存在并是一个目录
    * - -e file
      - 检查file是否存在
    * - -f file
      - 检查file是否存在并是一个文件
    * - -r file
      - 检查file是否存在并可读
    * - -s file
      - 检查file是否存在并非空
    * - -w file
      - 检查file是否存在并可写
    * - -x file
      - 检查file是否存在并可执行
    * - -O file
      - 检查file是否存在并归当前用户所有
    * - -G file
      - 检查file是否存在并且默认组与当前用户相同
    * - file1 -nt file2
      - 检查file1是否比file2新
    * - file1 -ot file2
      - 检查file1是否比file2旧

**复合条件测试：**

if语句支持两种布尔运算符：

::

    [ condition1 ] && [ condition2 ]
    [ condition1 ] || [ condition2 ]

if高级特性
~~~~~~~~~~~~~~~~~~~~~~

if语句支持两种高级特性：

- 双括号支持数学表达式
- 双方括号支持模式匹配

双括号命令提供了更多的数学运算符，其命令格式如下：

::

    (( expression ))

expression可以是任意的数学赋值或比较表达式，其中出现的大于号和小于号不需要转义。

在双方括号命令中可以使用正则表达式对字符串进行匹配，其命令格式如下：

::

    [[ expression ]]

    if [[ $USER == k* ]]

case语句
--------------------------

shell中的case语句格式如下：

.. code-block:: sh

    case variable in
    pattern1)               #如果符合条件1
        commands1;;
    pattern2 | pattern3)    #如果满符合条件2或者3
        commands2;;
    *)                      #else
        commands3;;
    esac

for语句
-------------------------

shell中的for语句格式如下：

.. code-block:: sh

    for var in list
    do
        commands
    done

实际工作中，for语句一般借助命令替换或者通配符进行读值。

借助命令替换读值：

.. code-block:: sh

    for file in `ls`
    do
        if [ -d "$file" ]
        then
            cd "$file"
            ls
            cd ..
        fi
    done

.. note::
    由于Linux允许目录和文件名中带有空格，所以在使用 ``$file`` 变量时将其用双引号圈起来，防止报错。

借助通配符读值：

.. code-block:: sh

    for file in $HOME/test/*
    do
        if [ -d "$file" ]
        then
            cd "$file"
            ls
            cd ..
        fi
    done

shell还支持C语言风格的for语句，格式如下：

.. code-block:: sh

    for ( variable assignment; condition; iteration process)
    do
        commands
    done

while语句
-----------------------

shell中的while语句的格式如下：

.. code-block:: sh

    while test command
    do
        other commands
    done

其中test *commands* 也支持方括号条件测试。

while语句还允许定义多个测试命令，但只有最后一个测试命令的退出状态码会被用于条件判断。

可以在for和while语句的done命令之后使用管道或进行重定向：

.. code-block:: sh

    for var in list
    do
        commands
    done > test_file

    while test command
    do
        other commands
    done | command

break和continue语句
---------------------------

shell中的break和continue语句接受单个参数以跳出多重循环，格式如下：

.. code-block:: sh

    break n
    continue n

其中n指定了要跳出的循环层数，默认为1，即跳出当前循环。

