
流程控制
============================================
Php流程控制简介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
任何 PHP 脚本都是由一系列语句构成的，正常情况下，代码就是按照编写的顺序从上往下逐行执行的，但并不是所有时候都希望程序顺序执行。
所谓流程控制，就是在代码逻辑中增加一些“开关”，亦即一些 **语句** 来 **控制整个流程**，让代码可以按照正常的业务需求运行到最后。

流程控制的三种结构
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **顺序结构**：不需人为控制，代码按照编写的顺序逐行执行
- **分支结构**：需要人为控制，根据既定条件判断结果，进而执行对应的预先设定的代码块
- **循环结构**：是代码高效解决重复问题的一种方式，让代码块在符合设定变化条件的前提下在指定范围内重复执行

分支结构
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1.  if分支结构(可无限层嵌套)

.. code-block:: PHP
    :linenos:  
        
    <?php 
      if (expr);        //括号内容按照布尔求值取true或false
      statement;        //true则执行，flase则跳过

.. code-block:: PHP
    :linenos:  
    
    <?php
    if ($a > $b) { 
      echo "a is greater than b";
    } else {          //否则执行该命令
      echo "a is NOT greater than b";
    }

.. code-block:: PHP
    :linenos:  

    <?php
    if ($a > $b) {
        echo "a is bigger than b";
    } elseif ($a == $b) {
        echo "a is equal to b";
    } else {
        echo "a is smaller than b";
    }

2. switch分支结构
   
   Switch也是一种通过特定条件匹配来选择执行代码块的分支结构，但是Switch的条件只有一个，且运行机制与if分支结构不一样。
   
   语法如下：
      .. code-block:: PHP
          :linenos:  
            
          <?php
          switch(表达式/条件变量){
          　　case 常量１:
          　　　　       //设定的满足该条件时执行的代码块;
          　　　　break; //结束分支结构，必须加，否则会继续执行下去
          　　case 常量2：
          　　　　       //设定的满足该条件时执行的代码块;
          　　　　break;
          　　...
          　　default:
          　　　　      //匹配不到任何条件以执行代码块;
          　　　　break;
          }
              
 
3. if与switch的区别：
    - if与switch的分支逻辑不大相同，if分支是逐个匹配并执行命令，而switch分支则是直接到达目标case，因此对于较多分支的情况下，switch效率要更高  
    - if分支要相对更加灵活，而switch只能是在既定的case中匹配

循环结构
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. while循环结构

.. code-block:: PHP
    :linenos:  

    <?php
    //输出1到50的整数
    $i = 1;            //定义初始化变量
    while($i <= 50){
        //循环体
        echo $i;       //如果到这结束，那么循环就进入死循环，因为$i永远为1不满足条件
        //变更循环条件
        $i++;          //在循环体中控制循环变量   
    }

.. code-block:: PHP
    :linenos:  

    <?php
    //求100以内的基数和
    $i = 1;
    $j = 0;            
    
    do{
        $j += $i;        //累计求和
        $i++;            //条件变更
    }while($i <= 100);   //条件判定
    echo $j;

2. for循环结构
  
.. code-block:: PHP
    :linenos:  
        
    <?php
    for ($i=1; $i<=5; $i++)
    {
        echo "Number：" . $i . PHP_EOL;
    }

3. foreach循环结构
    
foreach循环，是PHP中一种特定为数组设定的循环结构，能够方便的将数组的下标和值挨个取出来，从而实现对数组的所有元素的访问 **(遍历数组)** 。每进行一次循环迭代，当前数组元素的值就会被 **赋值** 给 $value 变量，并且数组指针会逐一地移动，直到到达最后一个数组元素。 
    
语法如下：
         .. code-block:: PHP
            :linenos:  
                
            <?php
            foreach ($array as $value)
            {
            code to be executed;
            }
 实例：
         .. code-block:: PHP
            :linenos:  
                
            <?php
            $colors = array("red","green","blue","yellow");
            **foreach** ($colors as $value) {
            echo "$value     //输出结果为数组中的所有元素"red","green","blue","yellow"
            ";


 循环控制中的特殊语句
 
 a. continue
       
    表示从continue以后的循环体 **本次** 不再执行， **重新开始** 下次循环
 b. break 
       
    表示跳出 **整个** 循环
    
 c. 优点：continue和break允许我们在循环内部设定特殊情况下的特殊执行方式，能使得循环流程更加灵活多变

协助流程控制的一些特殊函数/语句
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1. `declare(directive)`_: 控制代码的执行时间
   
.. _declare(directive): https://blog.csdn.net/u010324331/article/details/88316692
2. `return`_： 返回值，中断代码执行
   
.. _return: https://www.cnblogs.com/pxh-phper/p/6234626.html
3. `require()`_: 引入或者包含外部php文件,require_once则不会对已引用的文件再次引用

.. _require(): https://zhidao.baidu.com/question/534385892.html?qbl=relate_question_1&word=require%BA%AF%CA%FD%B5%C4%D7%F7%D3%C3%20php
4. `include`_: 包含并运行指定文件，include_once则不会对已包含的文件再次包含

.. _include: https://www.cnblogs.com/rainman/archive/2011/12/29/2305677.html
5. `goto`_: 跳转到程序中的另一标记了的目的位置 

.. _goto: https://www.cnblogs.com/phpper/p/9908860.html

   
