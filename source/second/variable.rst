
可变函数
============================================
可变函数
~~~~~~~~~~
当前有一个变量所保存的值，刚好是一个函数的名字，那么就可以使用变量+()来充当函数名使用。

可变函数应用举例(求5加10之后的四次方)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: php
    :linenos:

    <?php
     function calculate1($a,$b){
     $b=$b+10;
      return $a($b);
     }
     function calculate2($c){
      return $c*$c*$c*$c;
     }
     echo calculate1('calculate2',5)
     

输出结果如下： 50625

在echo calculate1('calculate2',5) 中，第一个传入的参数为另一个函数的函数名，第二个参数为需要进行处理的数字
calculate2()被calculate1()调用


将一个函数 **( calculate2() )** 传入给另一个函数 **( calculate1() )** 使用的过程叫回调过程。被传入的函数 **( calculate2() )** 也叫做回调函数。