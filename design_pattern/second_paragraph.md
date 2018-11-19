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

<br>

---

Tips: 

​	运行时：是一种面向对象的编译语言的运行环境

​	计算机程序运行的生命周期：OC是面向对象的动态语言，从源文件转换成计算机使用的机器语言，经过链接器链接之后形成了二进制的可执行文件，运行该程序的时候，就可以把二进制程序从硬盘载入到内存中并运行，包含编译时，链接时，运行时，加载时 （不同语言，不同系统不同，例如python为解释型语言，内置解释器将源代码转换为字节码，然后再由python解释器来执行这些字节码，所以无编译时，链接时，加载时。）

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>工厂方法</h3>

- **what** : 

  定义创建对象的接口，让子类决定实例化哪一个类

- **how** ：

  定义创建对象的接口，在其子类中实例化拥有一组共同行为的对象

- **why** ：

  使得一个累的实例化延迟到其子类，适用于无法准确预期生成结果时，或消除特有类的耦合

<br>

---

Tips:

​	工厂方法是创建对象的安全方法

​	通过子类重载并创建对象cocoa中常见的例子：

  - `[[SomeClass alloc] init]`
  - `[NSNumber numberWith*]`

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>抽象工厂</h3>

- **what** : 

  提供一个创建一系列相关或相互依赖对象的接口，而无需指定他们具体的类

- **how** ：

  通过对象（具体工厂）组合创建抽象对象

- **why** ：

  有多类共有相同的行为，但实际实现不同，则需要某种抽象类型作为其父类被继承

<br>

---

Tips:

​	软件设计的黄金法则： 变动需要抽象

​	当现有的抽象工厂需要支持新产品时，需要向父类添加相应的新工厂方法，同时修改其子类以支持新产品的新工厂方法。

抽象工厂 | 工厂方法

:————:|:————:

通过对象组合创建抽象产品|通过类继承创建抽象产品

创建多系列产品|创建一种产品

必须修改父类接口才能支持新产品|子类化创建者并重载工厂方法以创建