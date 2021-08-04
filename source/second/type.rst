
PHP的八种数据类型
============================================

php数据类型包括String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值），Resource（资源）。

PHP 字符串
--------------

字符串是连续的字符序列，由数字、字母和符号组成,字符串中的每个字符只占用一个字节。

字符串可以是引号内的任何文本。您可以使用单引号或双引号：

.. code-block:: php
  :linenos:

  <?php 
  $x = "Hello world!"; 
  $x = 'Hello world!';
  ?>

PHP 整数型（integar)
---------------------

整数是没有小数的数字。

整数规则：

-  整数必须有至少一个数字（0-9）
-  整数不能包含逗号或空格
-  整数不能有小数点
-  整数可以是正数或负数
-  可以用四种格式规定整数：十进制、十六进制（前缀是 0x）、八进制（前缀是 0）或二进制（前缀是 0b）

.. code-block:: php
  :linenos:

  <?php 
  $x = 5985;
  $x = -345; // 负数 
  $x = 0x8C; // 十六进制数
  $x = 047; // 八进制数
  $x = 0b11111111;//二进制数
  ?>

PHP 浮点型(float)
-------------------

浮点数是有小数点或指数形式的数字。

浮点数据类型可以用来存储数字，也可以保存小数。

.. code-block:: php
  :linenos:

  <?php 
  $x = 10.365; 
  $x = 2.4e3; 
  $x = 8E-5;
  ?>

PHP 布尔型(boolean)
----------------------

布尔变量是PHP变量中最简单的，逻辑是 true 或 false。

.. code-block:: php
  :linenos:

  $x=true;
  $y=false;

PHP 数组(array)
-------------------

数组是一组数据的集合，它把一系列数据组织起来，形成一个可操作的整体。

数组可以在一个变量中存储多个值。

.. code-block:: php
  :linenos:

  <?php 
  $cars=array("Volvo","BMW","Toyota");
  ?>

PHP 对象(object)
----------------
对象数据类型也可以用于存储数据。

在 PHP 中，对象必须声明。

首先，必须使用class关键字声明类对象。类是可以包含属性和方法的结构。

然后在类中定义数据类型，然后在实例化的类中使用数据类型：

.. code-block:: php
  :linenos:

  <?php

  class MyClass{
      public $age =100;
      }
      $obj =new MyClass
      echo $obj ->age;   //100

  ?>

PHP NULL 值
---------------

NULL 值表示变量没有值。NULL 是数据类型为 NULL 的值。

NULL 值指明一个变量是否为空值。 同样可用于数据空值和NULL值的区别。

可以通过设置变量值为 NULL 来清空变量数据

.. code-block:: php
  :linenos:

  <?php
  $x="Hello world!";
  $x=null;
  ?>

PHP 资源（resource）
-----------------------

PHP中的Resources不是确切的数据类型。这些基本用于存储对某些函数调用或外部PHP资源的引用。例如，考虑一个数据库调用，这是一个外部资源。

