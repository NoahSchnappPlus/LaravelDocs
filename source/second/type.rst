
PHP的八种数据类型
============================================

php数据类型包括String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值）。

PHP 字符串
-----------

字符串是字符序列，比如 "Hello world!"。

字符串可以是引号内的任何文本。您可以使用单引号或双引号：

.. code-block:: php
  :linenos:

  <?php 
  $x = "Hello world!";
  echo $x;
  echo "<br>"; 
  $x = 'Hello world!';
  echo $x;
  ?>

PHP 整数型
-----------

整数是没有小数的数字。

整数规则：

-  整数必须有至少一个数字（0-9）
-  整数不能包含逗号或空格
-  整数不能有小数点
-  整数正负均可
-  可以用三种格式规定整数：十进制、十六进制（前缀是 0x）或八进制（前缀是 0）

.. code-block:: php
  :linenos:

  <?php 
  $x = 5985;
  var_dump($x);
  echo "<br>"; 
  $x = -345; // 负数
  var_dump($x);
  echo "<br>"; 
  $x = 0x8C; // 十六进制数
  var_dump($x);
  echo "<br>";
  $x = 047; // 八进制数
  var_dump($x);
  ?>

PHP 浮点型
-----------

浮点数是有小数点或指数形式的数字。

.. code-block:: php
  :linenos:

  <?php 
  $x = 10.365;
  var_dump($x);
  echo "<br>"; 
  $x = 2.4e3;
  var_dump($x);
  echo "<br>"; 
  $x = 8E-5;
  var_dump($x);
  ?>

PHP 布尔型
--------------

逻辑是 true 或 false。

.. code-block:: php
  :linenos:

  $x=true;
  $y=false;

PHP 数组
----------

数组可以在一个变量中存储多个值。

.. code-block:: php
  :linenos:

  <?php 
  $cars=array("Volvo","BMW","Toyota");
  var_dump($cars);
  ?>

PHP 对象
----------
对象数据类型也可以用于存储数据。

在 PHP 中，对象必须声明。

首先，必须使用class关键字声明类对象。类是可以包含属性和方法的结构。

然后在类中定义数据类型，然后在实例化的类中使用数据类型：

.. code-block:: php
  :linenos:

  <?php
  class Car
  {
      var $color;
      function Car($color="green") {
        $this->color = $color;
      }
      function what_color() {
        return $this->color;
      }
  }

  function print_vars($obj) {
     foreach (get_object_vars($obj) as $prop => $val) {
       echo "    $prop = $val
  ";
     }
  }

  // instantiate one object
  $herbie = new Car("white");

  // show herbie properties
  echo "herbie: Properties
  ";
  print_vars($herbie);

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
  var_dump($x);
  ?>
