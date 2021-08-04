命名规则
==========================

**1、** **类的命名**

使用大写字母作为词的分割，其余的字母均为小写。

类名的首字母必须为大写英文字母。

类名命名不要使用下划线'_'。如：TestClass、User、UserType、ControllerAdmin。

**2、** **类属性的命名**

类的属性命名应该以字符'm'为前缀。

前缀'm'之后采用和类名一致的命名规则。

前缀'm'总是在名字的开头起到修饰的作用，就像'r'开头表示引用一样。如： mUserName、mUserKey 等。

**3、** **方法的命名**

方法要依赖于类对象，而函数不需要依赖于类对象。因此一般命名时注意区分方法和函数的命名，函数一般作为扩展文件引入。
方法的作用都是执行一个动作，达到一个目的。所以名称应该说明该方法是做什么的。一般名称的前缀都是有第一规律的，如is（判断）、get（得到），set（设置）。
方法的命名第一个单词的首字母小写，之后每个单词的首字母必须为大写。如：

.. code-block:: php
  :linenos:

  class UserModel
  {
      $mUserName = '';    //设置类的属性
      $mUserKey ='';   
 
      function getUser($userId)
     { //定义方法，得到用户信息
          ...
      }
  }

**4、** **方法中参数的命名**

第一个字符或第一个词必须为小写字母。

在第一个字符或第一个词之后的词都按照类命名的规则首字母大写。

.. code-block:: php
  :linenos:

  class User
  {
      function getUser($userId)
      {
          ...
      }
     
      function getMe(&$rUserKey)
      {
          ...
      }     
  }
　　

**5、** **引用变量**

引用变量要用 'r'前缀来修饰。如：$r_key = &$key;

**6、** **变量的命名**

一般所有字母都使用小写。

使用下划线'_'作为每个词的分割。

如： $msg_code、$msg_type、$msg_error 等。

临时变量通常使用 i、j、k、m、n,它们一般用于表示整形；c、d、e、s 它们一般用于字符型。

实例变量前需要用一个下滑线 '_'来修饰，首单词小写，其余的首字母大写

如：$_userType = new UserType() 。

**7、** **全局变量**

全局变量应该用前缀 'g'来修饰。如 ：global $gTest。

超全局变量 $GLOBALS['gTest2'] = '' 。

**8、** **常量和全局常量**

常量不能以 '$' 开头。

PHP常量是通过define()函数进行定义。

使用constant()函数获取常量值。

使用defined()函数判断常量是否定义。

使用get_defined_constants()获取所有当前已经定义的常量。

PHP中常用预定义常量。如：

1、__FILE__              程序文件名

2、__LINE__              程序所在行数

3、PHP_VERSION           PHP程序版本

4、PHP_OS                PHP解析器的操作系统

5、TRUE                  真值True

6、FALSE                 假值False

7、NULL                  null值

8、E_ERROR               指向最近的错误处

9、E_WARNING             指向最近的警告处

10、E_PARSE              解析语法有潜在问题处

11、NOTICE               发生异常，但不一定是错误处
 
　　
命名应该全部使用大写字母表示，用下滑线'_'来进行词的分割。如：

define('APP_VERSION', '1.1.0');

difine('APP_NAME', 'BRES');
 

**9、** **静态变量**

静态变量应该使用前缀 's' 来修饰。如：static $sName= '' 。

**10、** **函数的命名**

所有字母小写，多个单词之间用下滑线 '—' 分割。如：

.. code-block:: php
  :linenos:

  public function get_ip(){
      
      return $ip;
  }
　　
**11、** **各种命名规则可以组合一起来使用**

.. code-block:: php
  :linenos:

  class Example{
      static $msValue = "";        //该参数既是类属性，又是静态变量
      global $gmTst;             //声明静态全局变量
       
  }