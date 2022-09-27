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


    引用方式: `fig-ref`_


.. _fig-ref:

.. figure:: ./img.png
    :align: center
    :width: 200


`fig-ref`_

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

    引用方式：`table-ref`_

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

引用方式：`table-ref`_

3.5 引用文档
---------------

引用其他的rst文档时，省略后缀。

自定义引用文字：

::

    :doc:`引用文档 <../index>`

:doc:`引用文档 <../index>`

使用被引用文档的标题作为引用文字：

::

    :doc:`../index`

:doc:`../index`

3.6 使用标签引用文档
-----------------------

要在被引用的文件头定义标签，如index.rst文件头写 “index-label” 的标签。

::

    将下行标签写在index.rst首行
    .. _index-label:

    :ref:`使用标签引用文档 <index-label>`

    :ref:`index-label`

:ref:`使用标签引用文档 <index-label>`

:ref:`index-label`

4. 代码块
~~~~~~~~~~~~~~~~

4.1 基础代码块
----------------

行内代码块使用4个 \` 将代码包裹，两侧还需要有空格。

标记原始文本块需要使用两个连续的英文引号 :: ，之后跟空行，内容要缩进，再以空行结束。

4.2 highlight代码高亮
-----------------------

使用highlight定义默认高亮方式，直到下一个highlight指令才会更改高亮方式。

::

    .. highlight:: sh

    ::

        sudo apt install python

        echo "Hello world!"

效果：

.. highlight:: sh

::

    sudo apt install python
    echo "Hello world!"

4.3 code-block代码高亮
--------------------------

Shell 代码高亮：

::

    .. code-block:: sh  #指定语言
        :caption: test_shell  #标题
        :emphasize-lines: 2  #指定高亮行
        :linenos:   #显示行号

        sudo apt install python
        echo "Hello world!"

效果：

.. code-block:: sh
    :caption: test_shell
    :emphasize-lines: 2
    :linenos:

    sudo apt install python
    echo "Hello world!"

Python 代码高亮：

::

    .. code-block:: py
        :caption: test_py
        :emphasize-lines: 3, 4
        :linenos:

        def test():
            print("Hello world!")

        test()

效果：

    .. code-block:: py
        :caption: test_py
        :emphasize-lines: 3, 4
        :linenos:

        def test():
            print("Hello world!")

        test()

4.4 literalinclude嵌入本地文件并高亮
-----------------------------------------------------------

4.4.1 嵌入整个文件
++++++++++++++++++++

直接嵌入文件，包含标题、代码语言、高亮、带编号以及名称方便引用。

::

    .. literalinclude:: test.py
        :caption: test.py
        :language: py
        :emphasize-lines: 3, 4
        :linenos:

效果：

.. literalinclude:: test.py
        :caption: test.py
        :language: py
        :emphasize-lines: 3, 4
        :linenos:

4.4.2 嵌入文件的一部分
++++++++++++++++++++++++++++

通过lines指定嵌入文件的某些行。

::

    .. literalinclude:: test.py
        :caption: test.py
        :language: py
        :lines: 1, 2
        :linenos:

效果：

.. literalinclude:: test.py
        :caption: test.py
        :language: py
        :lines: 1, 2
        :linenos:

4.4.3 文件对比
++++++++++++++++++++++

::

    .. literalinclude:: test.py
    :diff: test2.py

效果：

.. literalinclude:: test.py
    :diff: test2.py

5. 特殊提示
~~~~~~~~~~~~~~~~~

- note: 注解（蓝）
- hint: 提示（绿）
- important: 重要（绿）
- tip: 小技巧（绿）
- warning: 警告（黄）
- caution: 警告（黄）
- attention: 注意（黄）
- error: 错误（红）
- danger: 危险（红）


::

    .. note:: This is a note admonition.
     This is the second line of the first paragraph.

     - The note contains all indented body elements
       following.
     - It includes this bullet list.

    .. hint:: This is a hint admonition.

    .. important:: This is a important admonition.

    .. tip:: This is a tip admonition.

    .. warning:: This is a warning admonition.

    .. caution:: This is a caution admonition.

    .. attention:: This is a attention admonition.

    .. error:: This is a error admonition.

    .. danger:: This is a danger admonition.

效果：

.. note:: This is a note admonition.
 This is the second line of the first paragraph.

 - The note contains all indented body elements
   following.
 - It includes this bullet list.

.. hint:: This is a hint admonition.

.. important:: This is a important admonition.

.. tip:: This is a tip admonition.

.. warning:: This is a warning admonition.

.. caution:: This is a caution admonition.

.. attention:: This is a attention admonition.

.. error:: This is a error admonition.

.. danger:: This is a danger admonition.