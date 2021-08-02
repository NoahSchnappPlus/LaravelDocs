请求流程
============================================

在Hello World实验中，从客户端输入URL（网址），到返回页面“Hello World！”的过程，
是一个HTTP请求响应过程。这是由一个最简单的Laravel路由定义实现的，涵盖了一个Web框架的基本功能：处理请求，返回响应。
本节将对于Laravel的请求流程展开介绍。

概述
~~~~~~~~~~~~

Laravel 请求流程（请求生命周期）概括起来主要分为四个主要阶段：

-  加载项目依赖
-  创建 Laravel 应用实例
-  接收请求并响应
-  发送响应与终止

要了解Laravel框架的整个运行过程，首先要看Laravel的入口文件public/index.php。

Laravel 应用的所有请求入口都是 public/index.php 文件。所有的请求都是经由 Web 服务器（Apache/Nginx）通过配置引导到这个文件，而四个阶段的处理也都发生在入口文件index.php中。

index.php 文件包含代码并不多，但是完成了一个请求从接收到响应的全部过程。

.. code-block:: php
  :linenos:
  
  //1.加载项目依赖
  require __DIR__.'/../vendor/autoload.php';
  
  //2.创建Laravel应用实例
  $app = require_once __DIR__.'/../bootstrap/app.php';

  //3.接收请求并响应
  $kernel = $app->make(Kernel::class);

  $response = tap($kernel->handle(
      $request = Request::capture()
  ))->send();                       //4.发送响应

  $kernel->terminate($request, $response);

请求到响应流程
~~~~~~~~~~~~~~~~~~~~

加载项目依赖
-----------------

PHP 依赖于 Composer 包管理器，入口文件通过注册加载 Composer 包管理器自动生成的class loader(类加载程序)，可以轻松注册并加载项目所依赖的第三方组件库。

所有组件的加载工作，由index.php中的这一行代码来完成：

.. code-block:: php
  :linenos:

  require __DIR__.'/../vendor/autoload.php';

创建 Laravel 应用实例
-------------------------

创建Laravel应用实例（即服务容器），由位于 bootstrap/app.php 文件里的引导程序完成，创建服务容器的过程就是应用初始化的过程，
主要实现了服务容器本身注册、基础服务提供者注册、核心类别名注册和基本路径注册。在注册过程中，服务容器会在对应属性中记录注册的内容，
以便在程序运行期间提供对应的服务，同时还会绑定 HTTP 内核及 Console 内核到 APP 容器。

创建Laravel应用实例的工作，由index.ph中的这一行代码来完成：

.. code-block:: php
  :linenos:
  
  $app = require_once __DIR__.'/../bootstrap/app.php';

接收请求并响应
--------------------

在完成Laravel应用实例（即服务容器）的创建后，开始处理请求，生成响应。

.. code-block:: php
  :linenos:

  $kernel = $app->make(Kernel::class);

  $response = tap($kernel->handle(
      $request = Request::capture()
  ))->send();

第1行为内核实例化的过程，在HTTP 内核 和 Console 内核 绑定到了 APP 容器之后，使用时通过 APP 容器 的 make() 方法将内核解析出来.

第3行到第5行为处理HTTP请求的过程，包含两个阶段：创建请求实例（第4行），处理请求（第3-5行）。handle() 方法接收一个 HTTP 请求，并最终生成一个 HTTP 响应。

发送响应与终止
-------------------

到这里，对HTTP请求的响应已经生成了，接下来以HTTP响应的形式发送给客户端，实现请求生命周期的最后环节。
响应的发送是通过“$response->send()；”实现的，发送响应由send()方法完成。

在完成HTTP响应的发送之后，接下来进入程序生命周期的最后阶段——程序终止，Laravel框架中，程序终止主要是完成终止中间件的调用。Web 服务器将等待下一轮用户请求。

本节介绍了请求到响应的整个执行过程，分别是加载项目依赖、创建 Laravel 应用实例、接收请求并响应、发送响应与终止。
每个阶段都有对应的职责功能，这就是Laravel框架的整个生命周期过程。