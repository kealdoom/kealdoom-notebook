reSturcturedText 快速入门
==========================

1. 标题、字体和段落
~~~~~~~~~~~~~~~~~~~~~~

1.1 标题
--------

- 可以表示标题的符号有 =、-、\`、:、’、"、~、^、_ 、* 、+、 #、<、> 。
- 对于相同的符号，有上标是一级标题，没有上标是二级标题。
- 标题最多分六级，可以自由组合使用。
- 全加上上标或者是全不加上标，使用不同的 6 个符号的标题依次排列，则会依次生成的标题为H1-H6。

::

    =========
    一级标题
    =========
    二级标题
    =========

    一级标题
    ~~~~~~~~~
    二级标题
    ---------
    三级标题
    +++++++++
    四级标题
    :::::::::
    五级标题
    #########
    六级标题
    ^^^^^^^^^

1.2 字体
---------

::

 *斜体*
 **粗体**
 ``高亮``

斜体：*斜体*

粗体：**粗体**

高亮：``高亮``

1.3 段落
----------

- 段落是被空行分割的文字片段，左侧必须对齐（没有空格，或者有相同多的空格）。

- 普通的文本段落之间，还有块级元素之间，必须使用一个空行加以区分，否则会被 reStructuredText 折叠到上一行。

2. 列表和表格
~~~~~~~~~~~~~

2.1 无序列表
-------------

符号列表可以使用 -、 \*、+ 来表示。
不同的符号结尾需要加上空行，下级列表需要有空格缩进。

::

    - 无序列表1
    - 无序列表2

        + 二级无序列表
    - 无序列表3

- 无序列表1
- 无序列表2

    + 二级无序列表
- 无序列表3

2.2 有序列表
------------

可以使用不同的枚举序号来表示有序列表，可用的枚举符号有：

::

    阿拉伯数字: 1, 2, 3, ... (无上限)。
    大写字母: A-Z。
    小写字母: a-z。
    大写罗马数字: I, II, III, IV, ..., MMMMCMXCIX (4999)。
    小写罗马数字: i, ii, iii, iv, ..., mmmmcmxcix (4999)。

还可以为枚举符号添加前缀和后缀：

::

    . 后缀: "1.", "A.", "a.", "I.", "i."。
    () 包起来: "(1)", "(A)", "(a)", "(I)", "(i)"。
    ) 后缀: "1)", "A)", "a)", "I)", "i)"。

枚举列表可以结合 # 自动生成枚举序号, 也可以只使用 # 。

::

    1. 有序列表1
    #. 有序列表2
    #. 有序列表3

    I. 有序列表1
    #. 有序列表2
    #. 有序列表3

    (A 有序列表1
    (# 有序列表2
    (# 有序列表3

    #. 有序列表1
    #. 有序列表2
    #. 有序列表3

1. 有序列表1
#. 有序列表2
#. 有序列表3

I. 有序列表1
#. 有序列表2
#. 有序列表3

(A) 有序列表1
(#) 有序列表2
(#) 有序列表3

#. 有序列表1
#. 有序列表2
#. 有序列表3

2.3 定义列表
------------

定义列表可以理解为解释列表，即名词解释。

条目占一行，解释文本要有缩进；多层可根据缩进实现。

::

    定义1
        内容1

    定义2
        内容2

定义1
    内容1

定义2
    内容2

2.4 字段列表
-------------

使用2个英文 : 将Key字段包裹：

::

    :标题: reSturcturedText 快速入门

    :日期: 27/09/2022

    :内容: reSturcturedText 基础语法


:标题: reSturcturedText 快速入门

:日期: 27/09/2022

:内容: reSturcturedText 基础语法

2.5 选项列表
-------------

选项列表是一个类似两列的表格，左边是参数，右边是描述信息。当参数选项过长时，参数选项和描述信息各占一行。

选项与参数之间有一个空格，参数选项与描述信息之间至少有两个空格。

::

    -a  example
    -b file  example
    -h  show help

-a  example
-b file  example
-h  show help

2.6 普通表格
---------------

::

    +------------+------------+-----------+
    | Header 1   | Header 2   | Header 3  |
    +============+============+===========+
    | body row 1 | column 2   | column 3  |
    +------------+------------+-----------+
    | body row 2 | Cells may span columns.|
    +------------+------------+-----------+
    | body row 3 | Cells may  | - Cells   |
    +------------+ span rows. | - contain |
    | body row 4 |            | - blocks. |
    +------------+------------+-----------+

+------------+------------+-----------+
| Header 1   | Header 2   | Header 3  |
+============+============+===========+
| body row 1 | column 2   | column 3  |
+------------+------------+-----------+
| body row 2 | Cells may span columns.|
+------------+------------+-----------+
| body row 3 | Cells may  | - Cells   |
+------------+ span rows. | - contain |
| body row 4 |            | - blocks. |
+------------+------------+-----------+

2.7 简单表格
------------

表格使用 == 号制作

::

    =====  =====  ======
       Inputs     Output
    ------------  ------
      A      B    A or B
    =====  =====  ======
    False  False  False
    True   False  True
    False  True   True
    True   True   True
    =====  =====  ======

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

2.8 列表表格
------------

**推荐使用列表式表格，修改方便**

::

    .. list-table:: Frozen Delights!
    :widths: 15 10 30
    :header-rows: 1

    * - Treat
      - Quantity
      - Description
    * - Albatross
      - 2.99
      - On a stick!
    * - Crunchy Frog
      - 1.49
      - If we took the bones out, it wouldn't be
        crunchy, now would it?
    * - Gannet Ripple
      - 1.99
      - On a stick!

.. list-table:: Frozen Delights!
    :widths: 15 10 30
    :header-rows: 1

    * - Treat
      - Quantity
      - Description
    * - Albatross
      - 2.99
      - On a stick!
    * - Crunchy Frog
      - 1.49
      - If we took the bones out, it wouldn't be
        crunchy, now would it?
    * - Gannet Ripple
      - 1.99
      - On a stick!

2.9 CSV 表格
-------------

::

    .. csv-table:: Frozen Delights!
    :header: "Treat", "Quantity", "Description"
    :widths: 15, 10, 30

    "Albatross", 2.99, "On a stick!"
    "Crunchy Frog", 1.49, "If we took the bones out, it wouldn't be
    crunchy, now would it?"
    "Gannet Ripple", 1.99, "On a stick!"

.. csv-table:: Frozen Delights!
    :header: "Treat", "Quantity", "Description"
    :widths: 15, 10, 30

    "Albatross", 2.99, "On a stick!"
    "Crunchy Frog", 1.49, "If we took the bones out, it wouldn't be
    crunchy, now would it?"
    "Gannet Ripple", 1.99, "On a stick!"

3. 超链接与引用
~~~~~~~~~~~~~~~

3.1 自动超链接
--------------

reStructuredText会自动将网址生成超链接。

::

    https://www.github.com

https://www.github.com

3.2 外部超链接
--------------

用锚文本显示超链接:

::

    行内显示：
    这是\ `一个超链接 <https://www.example.com>`_

    使用引用：
    这是\ `另一个超链接`_

    .. _另一个超链接: https://www.example.com

这是\ `一个超链接 <https://www.example.com>`_

这是\ `另一个超链接`_

.. _另一个超链接: https://www.example.com

3.3 内部超链接
--------------

每一级标题都会变成一个锚，可以直接创建跳转至指定标题的链接。

::

    跳转至 `reSturcturedText 快速入门`_

跳转至 `reSturcturedText 快速入门`_

3.4 引用图片、表格
-----------------------

在需要引用的图片、表格前面加上引用标签进行引用(内部超链接)。

**图片引用：**

::

    .. _fig-ref:

    .. figure:: ./img.png
        :align: center
        :width: 200


    引用方式： ref: `fig-ref`_


.. _fig-ref:

.. figure:: ./img.png
    :align: center
    :width: 200

引用方式： ref: `fig-ref`_

**表格引用：**

::

    .. _table-ref:

    .. table:: example-table

    =====  =====  ======
       Inputs     Output
    ------------  ------
      A      B    A or B
    =====  =====  ======
    False  False  False
    True   False  True
    False  True   True
    True   True   True
    =====  =====  ======

    引用方式：ref: `table-ref`_

    自定义引用名称：ref: `table1 <table-ref>`_

.. _table-ref:

.. table:: table-ref

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

引用方式：ref: `table-ref`_

自定义引用名称：ref: `table1 <table-ref>`_
