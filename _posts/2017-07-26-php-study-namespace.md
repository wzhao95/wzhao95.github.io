---
layout: post
title:  "namespace"
date:   2017-07-26
categories: PHP基础
tags: php
excerpt: 可以在同一个文件中定义不同的命名空间代码，全局的非命名空间代码与命名空间中的代码通过大括号的形式可以组合在一起
---

* content
{:toc}

之前没有系统学习过`PHP`语言，直接上手`TP`框架了，所以认为`namespace`和`use`是`TP`框架的一部分，最近学习语言模块的时候遇到了这个问题，所以汇总了一下。

####`PHP`中命名空间可以解决两类问题：
- 用户编写的代码与`PHP`内部的类、函数、常量或第三方类、函数、常量之间的名字冲突。
- 为很长的标识符名称（通常是为了缓解第一类问题而定义的）创建一个别名，提高代码的可读性。

**_在没定义命名空间的情况下，所有的常量、类、函数等都在全局空间下。_**

####命名空间
通过关键字`namespace`声明。可以在同一个文件中定义不同的命名空间代码，全局的非命名空间代码与命名空间中的代码通过大括号的形式可以组合在一起
```
<?php
# 命名空间TestA
namespace TestA{
    class TestA{}
    function test(){}
}

# 命名空间TestB
namespace TestB{
    class TestB{}
    function test(){}
}

# 全局的非命名空间
namespace{
    class TestC{}
    function test(){}
}
```
**子命名空间**
与目录和文件的关系很像，`PHP`命名空间也允许指定层次的命名空间的名称
```
<?php
namespace a\b\Test; 

?>
```

####命名空间的引入
通过关键字`use`引入，通过`as`定义别名

引入命名空间三种情况：
**非限定名称，或不包含前缀的类名称。**在命名空间为`a`下，使用`$a = new foo();`代表引用的是`a\foo`。在命名空间为全局的情况下，使用该方法则引用的是`foo`。
**限定名称，或包含前缀的名称。**在命名空间为`a`下，使用`$a = new b\foo();`代码引入的是`a\b\foo`。在命名为全局的情况下，使用该方法引入的是`b\foo`。
**完全限定名称，或包含了全局前缀操作符的名称。**在命名空间为`a`下，`$a = new \c\b\foo()`;这种情况下，总是引入为`c\b\foor`文件

_上述三种方式其实就是文件路径中绝对路径和相对路径。_

注意：访问任意全局类、函数或变量，都可以使用完全限定名称，例如`\strlen()`或者`\Exception`。

```
<?php
namespace foo;

use \A\B\TestA;    #导入命名空间
use \A\B\TestB as TB;    #导入命名空间，并别名为TB

?>
```

####`namespace`和`__NAMESPACE__`魔术常量
`namespace`用于定义命名空间，`__NAMESPACE__`是包含当前命名空间的字符串，在全局的情况下，它是一个空字符串`''`。






