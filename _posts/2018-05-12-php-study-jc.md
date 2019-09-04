---
layout: post
title:  "基础"
date:   2018-05-12
categories: PHP基础
tags: php
excerpt: PHP基础
---

* content
{:toc}

#### `PHP`简介
最初用于维护个人主页，简写为：`Personal HomePage`。
最后改为：`Hypertext Preprocessor`（超文本预处理器），于1994年诞生。

**优势**

1. 性能好，开发效率高
2. 跨平台（可以在不同的操作系统上运：`windows`/`linux`/`unix`）
3. 上手快，编辑简单，实用性强
4. 面向对象[`PHP 4`开始，目前完全支持面向对象]
5. 开放的源代码，所有的`PHP`源代码都可以得到
6. 成本低

注：`PHP`灵活，对程序员的约束太少，`PHP`默认是解释运行机制，所以很多问题在运行阶段才会发现。

**`B/S`结构和`C/S`结构**

   - `B/S`：`Browser-Server`，浏览器-服务器，通过浏览器访问，都可以看作`B/S`
   - `C/S`：`Client-Server`，客户端-服务器，通过客户端访问，比如`QQ`，微信

####`PHP`基础语法

**开始标记和结束标记**

- 告诉`PHP`开始和停止解析二者之间的代码，这使得`PHP`可以被嵌入到各种不同的文档中去。
- 如果是文件是纯`PHP`代码，最好在文件末尾删除`PHP`结束标记。

**指令分隔符**

    //指令分隔符：php和其他编程语言一样，在每个语句后用分号';'结束指令，一段PHP代码中的结束标记隐含一个分号，所以在一个PHP代码段中的最后一行可以不用分号结束。
     echo 'hello, world'."\n";

**注释**

    //单行注释：// #
    //多行注释： /* */
    
    echo "你好"."\n";  //单行注释
    echo "你也好"."\n";  #单行注释
    
    /*
     * 多行注释
     */
    echo "大家都好"."\n"; 

####变量

由一个美元符号`$`后面跟变量名来表示（变量名区分大小写）。
和其他编程语言一样，一个有效的变量名由字符或者下划线开头，后面跟上任意数量的字符、数字或者下划线（也可中文）。

`$this`是个特殊的变量，不能被赋值。

    //使用变量之前必须定义并进行赋值
    $a;  //定义后不赋值直接使用会报错：Undefined variable
    echo $a;
    
    //变量名区分大小写
    $var = "Bob";
    $Var = "Tom";
    echo $var."和".$Var."\n";

**传值赋值和引用赋值**

    /*
     * 传值赋值：当一个变量的值赋予另外一个变量的时候，改变其中一个变量的值，将不会影响到另外一个变量。
     * 引用赋值：新变量指向了原始变量，改动新的变量将影响到原始变量，反之亦然。（只有由名字的变量才能引用赋值，比如表达式就不可以）
     */
    $a = "Bob";
    $b = $a;  //传值赋值
    $b = 10;
    echo "a：".$a."\tb：".$b."\n";
    
    $c = &$a;  //引用赋值
    $c = 20;
    echo "a：".$a."\tc：".$c."\n";

**全局变量**

    /*
     * php
     * 在C语言中全局变量在函数中会自动生效，除非被局部变量覆盖。
     * php中全局变量在函数中使用时必须声明为global
     * $GLOBALS是一个关联数组，每一个变量为一个元素，键名对应对变量，值对应变量内容。
     */
    $a = 1;
    $b = 2;
    function Sum()
    {
        echo "a：".$a."\tb：".$b;  //不会有任何输出
    
        //方法一：使用global标识全局变量
        global $a, $b;
        echo "a + b = ".($a + $b)."\n";
    
        //方法二：使用$GLOBALS替代
        echo "a + b = ".($GLOBALS['a'] + $GLOBALS['b'])."\n";
    }
    Sum();

**静态变量**

    /*
     * 静态变量仅在局部函数域中存在，但当程序执行离开此作用域时，其值并不丢失。
     */
    //每次调用，$a都会重新定义赋初值，$b在编译期间初始化，以后不会重新定义。
    function Test1()
    {
        $a = 0;
        static $b = 0;
        static $c = 1+2;
    
        echo "a=".$a."\t"."b=".$b."\n";
        $a++;
        $b++;
    }
    
    for ($i = 0; $i < 10; $i ++)
    {
        Test1();
    }

**可变变量**

    /*
     * 可变变量：一个变量的变量名可以动态设置和使用。
     */
    
    $a = 'hello';
    $$a = "world";  //一个可变变量获取了一个普通变量的值作为这个可变变量的变量名
    
    echo "$a ${$a}"."\n";
    echo "$a $hello"."\n";

####常量
一旦被定义，就不能再改变或者取消定义
常量只能包含`boolean`，`integer`，`float`，`string`

常量和变量有如下不同：

- 常量前面没有美元符号`$`;
- 常量只能用`define()`函数定义，而不能通过赋值语句;
- 常量可以不用理会变量的作用域而在任何地方定义和访问;
- 常量一旦定义就不能被重新定义或者取消定义;
- 常量的值只能是标量类型;

**常量的定义**
`php5.3.0`后，除了使用函数`define()`之外，还可以使用关键字`const`来定义常量。

`const`和`define()`的区别：

- 版本差异，`php5.3.0`后才能使用`const`关键字，`define()`函数对所有版本兼容
-	定义位置差异：
    	`define()`函数定义的常量是在执行`define()`函数时定义的，可以在任何位置定义，无论是函数内或函数外
        `const`关键字定义的常量是编译时定义的，所以定义的时候必须处于最顶端的作用区域，不能在函数内部
- 对值的表达式支持差异
        `const`关键字定义的常量值的表达式中不支持运算符，`define()`函数可以支持
    

注意：使用`const`关键字定义常量必须处于最顶端的作用区域。因为用此方法是在编译时定义的，这就意味着不能在函数内，循环体内用`const`来定义常量。
    
```
define("A", "Hello, world");
echo "A = ".A."\n";
    
const B = "你好";
echo "B = ".B."\n";
```

**魔术常量**

`__LINE__`：文件中的当前行号
`__FILE__`：文件的完整路径和文件名
`__DIR__`：文件所在的目录
`__FUNCTION__`：函数名称
`__CLASS__`：类的名称
`__TRAIT__`：`Trait`的名字，包括其被声明的作用区域
`__METHOD__`：类的方法名
`__NAMESPACE__`：当前命名空间的名称