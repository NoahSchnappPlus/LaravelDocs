
常量
============================================
常量的基本概念
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
与变量相对，常量是一个简单值的标识符(名字)。如同其名称所暗示，在脚本执行期间该值 *不能改变* (除所谓魔术常量)。

PHP 常量通常用来 **存储** 一个不被改变也不希望变化的 **数据**，该数据只能是四种标量数据类型的数据：整型(integer)、浮点型(float)、字符串(string)、布尔型(Boolean)，不过从 PHP7 开始常量支持了数组(array)类型。

定义常量的两种方式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**1.  define( ) 函数**
  
语法如下：
    
   bool **define** ( string $name , mixed $value , [ bool $case_insensitive = false ] )

其中包含有三个参数：
     
 **name**：必选参数，常量名称，即标志符。
     
 **value**：必选参数，常量的值。与C语言不同，Php作为一种弱类型语言，不需要严格设定该值的类型，与变量类似。 
     
 **case_insensitive** ：可选参数，如果设置为TRUE，该常量则大小写不敏感。默认是大小写敏感的。

实例：

.. code-block:: PHP
    :linenos:

    <?php
      define("WELCOME","一起学习Php吧"); //默认大小写敏感
      echo WELCOME;                     //严格输入常量名称(不需要加$),正确
      echo '<br>';
      echo Welcome;                     //输入小写名称，错误

.. code-block:: PHP
    :linenos:
  
    <?php
      define("WELCOME", "一起学习Php吧", true);// 不区分大小写的常量名
      echo wElcOme;                           // 正常输出结果(不需要加$)

**2.  const关键字**

语法如下：
  
   **const** $name = mixed $value

其中包含有两个参数：

   **name**: 定义常量名称

   **value**: 常量的值  

实例：     

.. code-block:: PHP
    :linenos:

    <?php
      const  EXCELLENT= '212';
      echo EXCELLENT;         //输出：212
      echo excellet;          //PHP提示常量未定义

预定义常量和魔术常量
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**1.  预定义常量**
- `预定义常量`_ 即指PHP预先定义好的常量（具体常见类型见链接）
 
.. _预定义常量: https://www.57zxw.net/htmlphp/biji/73459.html

.. code-block:: PHP
    :linenos:

    <?php
      echo PHP_VERSION,'<br>';		//PHP版本号
      echo PHP_OS,'<br>';	        //PHP操作系统
      echo PHP_INT_MAX,'<br>';		//PHP中整型的最大值

**2.  魔术常量**
- `魔术常量`_ 同样是预先定义的，但实际上他们并不是常量，其值随着在代码中的位置改变而改变（具体常见类型见链接）

.. _魔术常量: https://cloud.tencent.com/developer/article/1737506

.. code-block:: PHP
  :linenos:

  <?php
    echo __LINE__,'<br>';		//获取当前行号
    echo __FILE__,'<br>';		//文件的完整路径和文件名
    echo __DIR__,'<br>';		//文件所在的目录

与常量相关的重要函数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**1.  constant()函数**

constant() 函数用于返回一个常量的值，若常量未被定义则返回NULL    
  
语法如下：

   constant($name即常量名)

.. code-block:: PHP
  :linenos:

  <?php
    define("WELCOME","HelloWorld!");
    echo constant("WELCOME");  //输出该常量名对应的值，HelloWorld!

**2.  defined()函数**
defined() 函数检查是否定义了某一常量，若常量存在则返回 TRUE，否则返回 FALSE

语法如下：

   defined($name即常量名)

.. code-block:: PHP
  :linenos:

  <?php
    define("WELCOME","HelloWorld!");
    if(defined("WELCOME"))      //如果已经定义了该常量，则defined函数返回true，否则返回false不执行该判断语句
    echo WELCOME;               //输出
  
**3.  补充NULL、FALSE与0的区别于联系**
 
`NULL vs FALSE vs 0 in Php`_

.. _NULL vs FALSE vs 0 in Php: https://stackoverflow.com/questions/137487/null-vs-false-vs-0-in-php

常量特点
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 常量一旦被定义就无法更改或撤销定义。
- 常量名不需要开头的$
- 与变量不同，常量贯穿整个脚本是自动 **全局** 的。 作用域(见2.12)不影响对常量的访问
- 常量值只能是字符串或数字
