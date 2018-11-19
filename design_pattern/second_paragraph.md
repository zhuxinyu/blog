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

---

<br>

|            抽象工厂            |             工厂方法             |
| :----------------------------: | :------------------------------: |
|  通过对象创建组合创建抽象产品  |      通过类继承创建抽象产品      |
|         创建多系列产品         |           创建一种产品           |
| 必须修改父类接口才能支持新产品 | 子类化创建者并重载工厂方法以创建 |

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>生成器</h3>

- **what** : 

  使一个复杂对象的构建与他的表现分离，使得同样的构建过程可以创建不同的表现

- **how** ：

  Client（客户）- director (指导者) - builder (生成器)

- **why** ：

  创建对象算法应独立于部件的装配方式

<br>

---

Tips:

​	生成器与抽象工厂最大的区别在于，生成器是多步，多方式构建，工厂以单一步骤，单一方式构建对象。

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>单例</h3>

- **what** : 

  保证一个类仅有一个实例，并提供一个访问他的全局访问点

- **how** ：

  借用父类处理底层内存分配

- **why** ：

  系统中只能共享而不能复制的资源

<br>

---

Tips:

- 子类化单例的技巧：`Singleton *singleton = [NSAllocateObject ([Singleton class], 0, NULL) init];`

​	第一个参数是singleton类的类型，第二个参数是用于索引的实例变量的额外字节数，它总是0，第三个参数用于指定内存中分配的区域，一般为NULL，表示默认区域

- 单例的线程安全：要让单例线程安全，可在静态实例的nil检查周围加入一些@synchronized()程序块或者NSLock实例，如果有其他属性需要保护，也可以把他们声明为atomic型
- Cocoa Touch中使用的单例模式：UIApplication(处理内存管理任务) / UIAccelerometer (加速度相关) / NSFileManager （文件管理器）

---

