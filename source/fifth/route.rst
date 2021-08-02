路由命名和分组
============================================

路由命名
~~~~~~~~~~
路由命名可以方便地为指定路由生成URL或者重定向。通过在路由定义上链式调用 **name** 方法可以指定路由名称。

.. code-block:: php 
  :linenos: 

  <?php
  Route::get('user/profile',function(){
       //闭包行为
  })->name('profile');
   
同时可以指定控制器行为的路由名称：

.. code-block:: php
  :linenos:

  <?php
  Route::get('user/profile',[UserProfileController::class,'show'])->name('profile');

**注意：路由器命名必须是唯一的**

生成指定路由的URL
---------------------
一旦为路由指定了名称，就可以使用全局辅助函数 **route** 来生成链接或者重定向到该路由：

.. code-block:: php
    :linenos:

    <?php
    //生成链接
    $url=route('profile');

    //生成重定向
    return redirect()->route('profile');

如果有定义参数的命名路由，可以把参数作为 **route** 函数的第二个参数传入，
指定的参数将会自动插入到URL中对应的位置

.. code-block:: php
    :linenos:

    <?php
    Route::get('user/{id}/profile', function ($id) {
                    //
    })->name('profile');

    $url = route('profile', ['id' => 1]);

如果在数组中传递额外的参数，这些键或值将自动添加到生成的 URL 的查询字符串中：

.. code-block:: php
    :linenos:

    <?php
    Route::get('user/{id}/profile', function ($id) {
                    //
    })->name('profile');

    $url = route('profile', ['id' => 1，'photos'=>'yes']);
         //   /user/1/profile?photos=yes


检查当前路由
----------------
如果你想判断当前请求是否指向了某个命名过的路由，你可以调用路由实例上的 **name** 方法。例如，你可以在路由中间件
中检查当前路由名称

.. code-block:: php
    :linenos:

    <?php
    public function handle($request, Closure $next)
    {
           if ($request->route()->named('profile')) {
                      //
    }

    return $next($request);
    }

路由分组
~~~~~~~~~~~
通常，一组路由会有一些特定的特征：比如，一定的认证要求、路径前缀，或者是控制器与命名空间等。
在每个路由上反复定义这些共同的特征不仅会显得很烦琐，还可能会改变路由文件的模型并影响应用程序的某些结构。

路由组允许多个路由组合在一起，并且可以将任何共享的配置应用于整个组，从而减少配置信息的重复。
此外，这些路由会被组合在一起，所以路由组也是未来开发者的可视化提示。

要将两个或多个路由组合在一起，需要将路由的定义放在路由组里面。
实际上，这是将闭包传递给路由组定义，并在闭包中定义分组的路由。

.. code-block:: php
   :linenos:
 
   <?php
   Route::group([],function(){             
        Route::get('hello',function(){
             return 'Hello';
        });

        Route::get('world',function(){
             return 'World';
        });
   });
   //路由组中的第一个参数为空数组，该空数组允许传递各种配置信息，这些配置将对该组内的所有路由生效

路由组最常见的功能就是将中间件应用于一组路由中，但是在其他方面，
路由组在Laravel中也常常被应用在权限控制方面，
比如，对用户进行验证以及对访客用户使用网站的某些内容进行限制等。

在示例中，将dashboard与account组成一个路由组，并且为该路由组建立一个中间件auth，
**auth** 中间件是laravel自带的用户认证中间件。
此时该中间件对dashboard与account这两者都会生效。
在此示例中，表示用户必须登录后才能查看控制中心（dashboard）或账户页面（account）。

.. code-block:: php
   :linenos:

    <?php
    Route::group(['middleware'=>'auth'],function(){
        Route::get('dashboard',function(){
             return view('dashboard');
        });
    Route::get('account',function(){
             return view('account');
        });
    });

路径前缀
-----------
如果有一组路由需要共享某个路径段，可以用路由组简化此结构

.. code-block:: php
   :linenos:

   <?php
   Route::group(['prefix'=>'api'],function(){
        Route::get('/',function(){
             //设置路径为 /api
        });
        Route::get('users',function(){
             //设置路径为 /api/users
        });
   });

子域名路由
---------------
子域名路由与路由前缀一样，但是作用域不同：子域名路由的作用域是子域名，而不是路由前缀。这主要有两个作用。
首先，可以在不同的子域名中展示应用程序中的不同部分（或完全不同的应用程序）。

.. code-block:: php
   :linenos:

   <?php
   Route::group(['domain'=>'api.myapp.com'],function (){
        Route::get('/',function(){
            //
        });
   });

其次，可以将子域名的某一部分设置为参数。
通常，这在多租户技术的案例中用的比较多（例如Slack或Harast，其实每个公司都有自己的子域名，例如tighten.slack.co）。

.. code-block:: php
   :linenos:

   <?php
   Route::group(['domain'=>'{account}.myapp.com'],function(){
        Route::get('/',function($account){
                  //
        });
        Route::get('users/{id}',function ($account,$id){
                 //
        });
   });

需要注意的是，路由组中的任何参数都将通过第一个参数传递到路由组内各路由的方法中。

命名空间前缀
-----------------
当按照子域名或者路由前缀的方式对路由进行分组时，它们的控制器可能会有相同的PHP命名空间。
在API的示例中，所有的API路由的控制器都可能在一个API命名空间内。通过使用路由组命名空间前缀，
就可以避免在群组内使用很长的控制器进行引用，如"API/ControllerA@index"以及"API/ControllerB@index"。

.. code-block:: php
   :linenos:

   <?php
   // App\Http\Controllers\ControllerA
   Route::get('/','ControllerA@index');

   
   Route::group(['namespace'=>'API'],function(){
   // App\Http\Controllers\API\ControllerB
        Route::get('api/','ControllerB@index');
   });

名称前缀
----------
前缀并不仅局限于此。通常，路由名称会反映路径元素的继承链（inheritance chain），
因此，users/comments/5将会由名为users.comments.show的路由实现。
在这种情况下，在users.comments资源下面的所有路由中使用路由组是很常见的。
就像可以使用前缀URL字段和控制器命名空间一样，也可以在路由名称前面加上前缀字符串。
使用路由组名称前缀，可以定义该组中的每个路由，让它们都有一个给定的字符串作为其名称前缀。
在这种情况下，我们会将前缀“users.”添加到每个路由名称前，然后添加“comments.”。

.. code-block:: php
   :linenos:
   
   <?php
   Route::group(['as'=>'users.','prefix'=>'users'],function(){
        Route::group(['as'=>'comments.','prefix'=>'comments'],function(){
                      //路由名称将是users.comments.show
             Route::get('{id}',function(){
                          //
             })->name('show');
        });
   });