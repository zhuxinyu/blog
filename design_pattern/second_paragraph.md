<h1>第二部分 对象创建的设计模式</h1>

> 概要
>
> > - 原型 prototype
> > - 工厂方法 virtual constructor
> > - 抽象工厂 abstract factory
> > - 生成器 client-director-builder
> > - 单例 singleton

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>原型</h3>

- **what** : 

  使用原型实例指定创建对象的种类，并通过赋值这个原型创建新的对象

- **how** ：

  deepCopy (Cocoa中使用NSCoping协议 )

- **why** ：

  相关类其行为略有不同，而且主要差异在于内部属性，或作为同意环境下其他相关事物的基础

---

Tips: 

​	运行时：是一种面向对象的编译语言的运行环境

​	计算机程序运行的生命周期：OC是面向对象的动态语言，从源文件转换成计算机使用的机器语言，经过链接器链接之后形成了二进制的可执行文件，运行该程序的时候，就可以把二进制程序从硬盘载入到内存中并运行，包含编译时，链接时，运行时，加载时 （不同语言，不同系统不同，例如python为解释型语言，内置解释器将源代码转换为字节码，然后再由python解释器来执行这些字节码，所以无编译时，链接时，加载时。）

---



<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>工厂方法</h3>

- **what** : 

  定义创建对象的接口，让子类决定实例化哪一个类

- **how** ：

  定义创建对象的接口，在其子类中实例化拥有一组共同行为的对象

- **why** ：

  使得一个累的实例化延迟到其子类，适用于无法准确预期生成结果时，或消除特有类的耦合



---

Tips:

​	工厂方法是创建对象的安全方法

​	通过子类重载并创建对象cocoa中常见的例子：

  - `[[SomeClass alloc] init]`
  - `[NSNumber numberWith*]`

---



