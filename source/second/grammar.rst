PHP语言基础
============================================

PHP是一款功能强大的嵌入式HTML脚本语言，经常被程序员用来作为网站开发的基础语言。
PHP语法基础知识点包括PHP脚本代码标记、PHP指令分隔符、PHP的注释和PHP的输出。

基础PHP语法
~~~~~~~~~~~~~~~~

PHP 脚本可以放在文档中的任何位置。

PHP 脚本以 <?php 开始，以 ?> 结束：

.. code-block:: php
  :linenos:

  <?php
  // PHP 代码
  ?>

PHP 文件的默认文件扩展名是 ".php"。

PHP 文件通常包含 HTML 标签以及一些 PHP 脚本代码。

下面的例子是一个简单的 PHP 文件，其中包含了使用内建 PHP 函数 "echo" 在网页上输出文本 "Hello World!" 的一段 PHP 脚本：

实例
-------

.. code-block:: php
  :linenos:

  <!DOCTYPE html> 
  <html> 
  <body> 

  <h1>My first PHP page</h1> 

  <?php 
  echo "Hello World!"; 
  ?> 
 
  </body> 
  </html>

PHP 中的每个代码行都必须以分号结束。分号是一种分隔符，用于把指令集区分开来。

通过 PHP，有两种在浏览器输出文本的基础指令：echo 和 print。

PHP标记风格
~~~~~~~~~~~~

**1.** **XML风格：**

.. code-block:: php
  :linenos:

  <?php
  echo “这是XML风格标记”;
  ?>

**2.** **脚本风格：**

.. code-block:: php
  :linenos:

  <script language=”php”>
  echo “这是脚本风格标记”;
  </script>

**3.** **简短风格：**

.. code-block:: php
  :linenos:

  <? echo “这是XML风格标记”; ?>

**4.** **ASP风格：**

.. code-block:: php
  :linenos:
  
  <%
  echo “这是ASP风格标记”;
  %>

PHP中的注释
~~~~~~~~~~~~

PHP 代码中的注释不会被作为程序来读取和执行。它唯一的作用是供代码编辑者阅读。

实例
-------

.. code-block:: php
  :linenos:

  <!DOCTYPE html>
  <html>
  <body>

  <?php
  // 这是 PHP 单行注释
  # 这是PHP单行注释

  /*
  这是 
  PHP 多行
  注释
  */
  echo "Hello World!";
  ?>

  </body>
  </html>


