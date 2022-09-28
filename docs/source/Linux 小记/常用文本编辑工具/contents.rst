常用文本编辑工具
=======================

sed
-------------

Not Implement

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
-f file  从指定的文件中读取gawk程序
-v var  在gawk程序中定义一个变量及其默认值


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
        kealdoom
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

默认情况下，OFS为一个空格，print命令会自动将OFS变量的值放置在输出的每个字段之间，可以通过设置OFS变量，使得以任意字符串分隔输出。

.. code-block:: sh

    $ cat file2
        data11,data12,data13,data14,data15
        data21,data22,data23,data24,data25
        data31,data32,data33,data34,data35
    $

    $ gawk 'BEGIN {FS=","} {print $1, $2, $3}' file2
        data11 data12 data13
        data21 data22 data23
        data31 data32 data33
    $

    $ gawk 'BEGIN {FS=","; OFS="-"} {print $1, $2, $3}' file2
        data11-data12-data13
        data21-data22-data23
        data31-data32-data33
    $

对于定长格式的数据文本，可以选择FIELDWIDTHS变量进行分隔。

FIELDWIDTHS变量可以通过字段宽度匹配数据，一旦设置了FIELDWIDTHS变量，FS就会失效。

.. code-block:: sh

    $ cat file3
        1234567890
        1.23456789
        123.456^789
    $

    $ gawk 'BEGIN{FIELDWIDTHS="3 3 3 3"} {print $1,$2,$3,$4}' file3
        123 456 789 0
        1.2 345 678 9
        123 .45 6^7 89
    $

变量RS和ORS定义了gawk程序如何分隔记录，默认设置为换行符，即输入数据流中的每行文本都被视为一条记录。

如果处理数据过程中遇到多行的字段，可以把RS设置为空字符串，此时gawk会把每个空白行当作一个记录分隔符。

.. code-block:: sh

    $ cat file4
        I am
        record1

        I am
        record2

        I am
        record3
    $

    $ gawk 'BEGIN{FS="\n"; RS=""} {print $2}' file4
        record1
        record2
        record3
    $

除了字段和记录分隔符变量外，gawk还提供了其他一些内建变量，这里列出一些常用内建变量：

.. list-table:: 更多的gawk常用内建变量
    :widths: 10, 40
    :align: center
    :header-rows: 1

    * - 变量
      - 描述
    * - ARGC
      - 当前命令行参数个数
    * - ARGV
      - 包含命令行参数的数组
    * - ENVIRON
      - 当前shell环境变量及其值组成的关联数组
    * - NF
      - 单个记录中的字段总数
    * - NR
      - 已处理的输入记录数
    * - FNR
      - 当前数据文件已处理的输入记录数

使用ARGC和ARGV参数可以获得相对应的参数信息。

.. code-block:: sh

    $ gawk 'BEGIN{print ARGC,ARGV[0],ARGV[1]}' file1
        2 gawk file1
    $

.. note::

    - gawk不会把引号中的程序脚本视为命令行参数的一部分；
    - ARGV数组索引从0开始；
    - 在脚本中引用gawk变量时，变量名前不需要加美元符$。

ENVIRON变量使用关联数组提取shell环境变量的值，数组索引为环境变量名

.. code-block:: sh

    $ gawk 'BEGIN{print ENVIRON["HOME"]; print ENVIRON["SHELL"]}'
        /home/kealdoom
        /bin/bash
    $

变量NF，NR，FNR用于在gawk程序中跟踪数据字段和记录。

NF变量包含记录中最后一个数据字段的数字值，在NF前加上美元符可以将其用作字段变量：

.. code-block:: sh

    $ gawk 'BEGIN{FS=":"; OFS=":"}{print $1,NF}' /etc/passwd
        root:7
        kealdoom:7
    $

    $ gawk 'BEGIN{FS=":"; OFS=":"}{print $1,$NF}' /etc/passwd
        root:/bin/bash
        kealdoom:/bin/bash
    $

FNR变量包含当前数据文件已处理过的记录数，NR变量包含已处理过的数据总数。

.. code-block:: sh

    $ gawk 'BEGIN{FS=","}{print $1,"FNR="FNR}' file1 file1
        data11 FNR=1
        data21 FNR=2
        data31 FNR=3
        data11 FNR=1
        data21 FNR=2
        data31 FNR=3
    $

    $ gawk '
    > BEGIN{FS=","}
    > {print $1,"FNR="FNR,"NR="NR}' file1 file1
        data11 FNR=1 NR=1
        data21 FNR=2 NR=2
        data31 FNR=3 NR=3
        data11 FNR=1 NR=4
        data21 FNR=2 NR=5
        data31 FNR=3 NR=6
    $

自定义变量
*****************

gawk允许自定义变量，可以在脚本或者命令行中为变量赋值。

.. code-block:: sh

    $ gawk '
    > BEGIN{
    > testing="This is a test"
    > print testing
    > testing=42
    > print testing
    > }'
        This is a test
        42
    $

    $ gawk 'BEGIN{x=4; x= x * 2 + 3; print x}'
        11
    $

    $ cat script1
        BEGIN{FS=","}
        {print $n}
    $

    $ gawk -f script1 n=2 file1
        data12
        data22
        data32
    $

如果希望自定义变量值在BEGIN部分可用，可以添加-v选项。

.. code-block:: sh

    $ gawk -v n=2 -f script1 file1
        data12
        data22
        data32
    $

数组
~~~~~~~~~~~~~

gawk中的数组变量赋值格式：

*var[index] = element*

其中var是数组名，index为索引值（任意字符串），element是数据元素值，下面是一些具体例子：

.. code-block:: sh

    $ gawk 'BEGIN{
    > var["one"] = 1
    > var["two"] = 2
    > total = var["one"] + var["two"]
    > print total
    > }'
        3
    $

     $ gawk 'BEGIN{
    > var[1] = 1
    > var[2] = 2
    > total = var[1] + var[2]
    > print total
    > }'
        3
    $

还可以使用 ``for`` 语句对数组进行遍历：

.. code-block:: sh

    $ gawk 'BEGIN{
    > var["a"] = 1
    > var["g"] = 2
    > var["m"] = 3
    > var["u"] = 4
    > for (test in var)
    > {
    >   print "Index:",test," - Value:",var[test]
    > }
    > }'
        Index: u  - Value: 4
        Index: m  - Value: 3
        Index: a  - Value: 1
        Index: g  - Value: 2
    $

.. note::
    由于gawk数组由散列表实现，索引值不会按期望顺序返回，但索引值和数据值是对应的，

可以使用delete语句删除数组索引：

::

    delete array[index]

匹配模式
~~~~~~~~~~~~~~~

gawk支持正则表达式，在使用正则表达式时，正则表达式必须出现在它要控制的程序脚本的左花括号前。

.. code-block:: sh

    $ gawk 'BEGIN{FS=","} /11/{print $1}' file1
        data11
    $

匹配操作符允许将正则表达式限定在记录中的特定数据字段。匹配操作符是波浪线，可以指定匹配操作符、数据字段变量以及要匹配的正则表达式，如：

::

    $1 ~ /^data/

其中$1变量代表记录中的第一个数据字段，这个表达式会匹配第一个字段以data开头的所有记录。

下面是一些具体使用匹配操作符的例子：

.. code-block:: sh

    $ gawk 'BEGIN{FS=","} $2 ~ /^data2/{print $0}' file1
        data21,data22,data23,data24,data25
    $

    $ gawk -F: '$1 ~ /kealdoom/{print $1,$NF}' /etc/passwd
        kealdoom /bin/bash
    $

也可以使用!号来排除正则表达式匹配：

::

    $1 !~ /expression/

除了正则表达式之外，还可以使用任何常见的数学比较表达式：

- x == y
- x <= y
- x < y
- x >= y
- x > y

具体示例如下：

.. code-block:: sh

    $ gawk -F: '$7 == "/bin/bash"{print $1}' /etc/passwd
        root
        kealdoom
    $

结构化命令
~~~~~~~~~~~~~~~~

gawk支持常见的结构化编程命令。

if语句格式：

::

    if (condition)
    {
        statements
    }
    else
    {
        statements
    }

    if (condition) statement1; else statement2

while语句格式：

::

    while (condition)
    {
        statements
    }

while语句中也支持使用break, continue跳出循环。

do-while语句格式：

::

    do
    {
        statements
    } while (condition)

for语句:

::

    for ( variable assignment; condition; iteration process)
    {
        statements
    }

格式化打印
~~~~~~~~~~~~~~~

gawk中 ``printf`` 的用法与C语言一样。

.. code-block:: sh

    $ gawk 'BEGIN{
    > x = 10 * 100
    > printf "The answer is: %e\n", x
    > }'
        The answer is: 1.000000e+03
    $
