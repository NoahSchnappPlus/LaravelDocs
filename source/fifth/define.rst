路由的定义与重定向
============================================

路由的概念
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
路由用来将用户的请求按照 **事先规划好的方案** 提交给指定的控制器，或者功能函数来进行处理。

简单来说，路由就是访问的地址形式。在我们搭建好laravel框架后再浏览器输入localhost为什么就能呈现欢迎界面，这实际上是由于在路由文件中已经定义好了路由，这个路由被称为跟路由。
可以看出，路由是外界访问Laravel应用程序的通路或者说其定义了Laravel向外界提供服务的具体方式。此处对于概念感到不理解也没有关系，在接下来的路由学习过程中再反复回头来看定义就会发现清晰了很多。

对路由的定义主要在搭建的laravel框架下的路由文件routes/web.php内进行。文件具体内容见5.3目录结构，下述操作都在该路由文件下进行。

路由的定义方式
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

路由的基本定义方式如图：

.. figure:: /media/rst_define/define.png
    :alt: define
    :align: center

可以看见，最简单的路由定义包括了

1. Route::请求方法
2. 请求的URL路径
3. 闭包或控制器

所有复杂的路由定义都是在这些基本组成成分上做进一步的升华，我们将在路由学习过程中陆续掌握。

URL路径
--------------------------------------------
关于URL路径在第四章HELLO WORLD实验中其实就有体现，URL路径的设定帮助人们更好的清晰记住网站而非由一串不规律数字组成的地址。

路由动作（请求方式）
--------------------------------------------
Route::（路由动作）  该语法的意义就是匹配某种请求路由，具体有如下几种

.. code-block:: PHP
    :linenos:

    <?php
    Route::get(‘/’,function(){});
    Route::post('/', function () {}); 
    Route::put('/', function () {});
    Route::delete('/', function () {});

此外还可通过route::any的方式定义一个可以捕获任何请求的路由，一般不建议这样定义。

为了兼顾便利性，我们可以用如route::match指定请求方式，如这个路由就可以匹配两种请求Route::match(['get', 'post'], '/', function () {});

闭包和控制器
--------------------------------------------
闭包应该是在php学习中就很熟悉的概念了，关于控制器的内容可以参考 
`控制器学习 <https://blog.csdn.net/asdfghjkl45786/article/details/105741317>`_

路由参数
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
路由参数可以理解为可变的URL地址段，在路由中定义路由参数后，该值可以传递给闭包，具体可以分为如下几种类型

必选参数
--------------------------------------------

.. code-block:: PHP
    :linenos:

    <?php
    Route::get('user/{id}', function (id) { return 'User ' .id;
    });

在浏览器里访问user/1就可以得到：User 1；若只输入user则会报错，参数必选

定义多个参数：

.. code-block:: PHP
    :linenos:

    <?php
    Route::ger('posts'/{post},'comments'/{comment},function($postId,$commentId){
    return $postId. '-'.$commentId;
    });

可选参数
--------------------------------------------
可选参数绑定使得路由变得更灵活

.. code-block:: PHP
    :linenos:

    <?php
    Route::get('user/{name?}', function ($name = null) {  //在参数后加？则为可选参数
    return ‘name: ’.$name;
    }); 
    //访问user/ 输出结果 name:               //不输入参数则按设定的默认赋值
    Route::get('user/{name?}', function ($name = 'John') {
    return $name; //output:John 
    });
    //访问user/Olivia 输出结果 name: Olivia  //输入参数则赋值给方法

正则约束过滤
--------------------------------------------
关于正则表达式的相关知识见 
`正则表达式 <https://www.runoob.com/regexp/regexp-intro.html>`_
利用where关键字为路由参数设定正则匹配规则，从而起到约束过滤的效果。常见类型如下


.. code-block:: PHP
    :linenos:

    <?php
    Route::get('page/{id}', function ($id) {
        return '页面ID: ' . $id;
    })->where('id', '[0-9]+');

    Route::get('page/{name}', function ($name) {
        return '页面名称: ' . $name;
    })->where('name', '[A-Za-z]+');

    Route::get('page/{id}/{slug}', function ($id, $slug) {
        return $id . ':' . $slug;
    })->where(['id' => '[0-9]+', 'slug' => '[a-zA-Z]+']);

重定向
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

应用情形
--------------------------------------------

重定向 (Redirect)就是通过各种方法将各种网络请求重新定个方向转到其它位置（如：网页重定向、域名的重定向、路由选择的变化也是对数据报文经由路径的一种重定向）。
我们在网站建设中，时常会遇到需要网页重定向的情况：

1. 网页被移到一个新地址； 
#. 网站调整（如改变网页 目录结构）；
#. 网页扩展名改变(如应用需要把.php改成.Html)。

这种情况下，如果不设定重定向，则用户收藏夹或搜索引擎数据库中旧地址只能让访问客户得到一个404 页面错误信息，丢失访问流量；再者某些注册了多个域名的网站，也需要通过重定向让访问这些域名的用户自动跳转到主站点等。

具体实现
--------------------------------------------
1.	Meta标签实现

.. code-block:: PHP
    :linenos:

    <?php
    if (!empty($url))    //$url为将重定向到的地址
    {
    echo '<meta http-equiv="refresh" content="0;url= $url">'; //表示在当前页面停留0秒后跳转到目标页面
    }

2.	Php页面重定向实现

.. code-block:: PHP
    :linenos:

    <?php
    header('Location: https://www.baidu.com')；   //location后有一个空格

3.	利用脚本来实现

.. code-block:: PHP
    :linenos:

    <?php
    echo '<script>window.location.href = 'https://www.baidu.com';</script>';

几点提醒
--------------------------------------------
1. 建议删除除此重定向脚本外所有代码。
2. 在新页面上提到用户应更新其链接和书签。
3. 使用此代码创建一个重定向用户的下拉菜单。
