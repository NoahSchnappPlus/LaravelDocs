表单传值
============================================
表单（Form）用来负责数据采集功能。表单传值即浏览器通过表单元素将用户的选择或者输入的数据提交给后台服务器语言。
在表单传值过程中，Get与Post是两种不同的提交方式。

HTTP 定义了与服务器交互的不同方法，在客户端和服务器之间进行请求-响应时，两种最常被用到的方法是：GET 和 POST。

为什么使用表单传值
~~~~~~~~~~~~~~~~~~~~~
动态网站（Web2.0）的特点就是后台根据用户的需求定制数据，所谓的“需求”就是用户通过当前的选择或者输入的数据信息，表单就是这些数据的承载者。

下面通过一个范例来演示表单方式传值的效果和两者的区别。第一步：在app/Models使用命令新建控制器TestController；第二步：在resource/view中新建视图test.blade.php；
第三步：在web.php中定义路由，返回响应视图“test.blade.php”，引入控制器TestController中的方法。

Get传值
~~~~~~~~~~

Get表单方式的基本设定：<form method="GET">表单元素</form>

浏览网页http://localhost/test/form，页面效果：

.. figure:: media/postvalue001.png
  :align: center
  :alt:

  图4-2-1 Get传值form页面

点击提交按钮后，显示结果为

.. figure:: media/postvalue002.png
  :align: center
  :alt:

  图4-2-2 Get传值提交页面

Post传值
~~~~~~~~~~~~

Post表单方式的基本设定：<form method="POST">表单元素</form>



浏览网页http://localhost/test/form，页面效果：

.. figure:: media/postvalue001.png
  :align: center
  :alt:

  图4-2-3 Post传值form页面

点击提交按钮后，显示结果为

.. figure:: media/postvalue003.png
  :align: center
  :alt:

  图4-2-4 Post传值提交页面

Get请求通过URL传递表单值，服务端文件名后跟着“？”，表单元素name属性的值=用户输入的值（value属性的值），如果要提交多个属性值用&分隔开。

Post请求通过URL看不到提交的表单的值，在服务端用Form来接收数据。 

Get传值和Post传值区别
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1、Get传输的数据主要用来获取数据，不改变服务器上资源：Get只是用来获取内容。

2、Post传输的数据主要用来增加数据，改变服务器上资源：POST会改变服务器上数据内容。

3、get 传递的参数是可见的，post 是不可见的，post 更安全 

Get是不安全的，因为在传输过程，数据被放在请求的URL中。另外，用户也可以在浏览器上直接看到提交的数据，一些系统内部消息将会一同显示在用户面前。 
Post的所有操作对用户来说都是不可见的。

4、Get传输的数据量小，Post传输数据量无限制 

Get传输的数据量小，这主要是因为受URL长度限制； Post可以传输大量的数据，所以在上传文件只能使用Post。

5、传输的数据格式不同 

get传输简单数据(数值/字符串)，post可以提交复杂数据(数值/字符串/二进制等)

6、Get是Form的默认方法。

PHP接收数据的方式
~~~~~~~~~~~~~~~~~~

PHP接收数据的方式有三种：$_GET、$_POST、$_REQUEST，都是PHP超全局预定义数组，表单元素的“name”属性的值作为数组的下标，而value属性对应的值就是数组的元素值。

-  $_GET方式：接收GET方式提交的数据
-  $_POST方式：接收POST方式提交的数据
-  $_REQUEST方式：接收POST或者GET提交的所有数据