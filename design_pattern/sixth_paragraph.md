<h1>第六部分 行为扩展</h1>

> 概要
>
> > - 访问者 visitor
> > - 装饰 decorator
> > - 责任链 chain of responsibility

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>访问者</h3>

- **what** : 

  表示一个作用于某对象结构中的各元素的操作，它让我们可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

- **how** ：

  根据要访问的组合对象定义一组操作由一个协议来控制这组操作，这个协议就叫visitor，visitor的特点是可以访问组合的任意对象

- **why** ：

  1. 想对一个组合体实施一些依赖于其具体类型的操作（visitor与对象是耦合的，相当于定制操作）
  2. 需要对一个组合结构中的对象进行很多不相关的操作，但是不想让这些操作污染这些对象的类。可以将相关的操作集中起来，定义在一个访问者类中，并在需要在访问者中定义的操作时使用它
  3. 对于定义复杂结构的类很少作修改，但经常需要向其添加新的操作

<br>

---

Tips

- 缺点： visitor与对象结构、类型的耦合性较高
- 可用范畴替代访问者模式

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>装饰</h3>

- **what** : 

  动态地给一个对象添加一些额外的职责。就扩展功能来说，装饰模式比生成子类更为灵活。

- **how** ：

  1. 通过真正的子类实现装饰 (抽象类型)
  2. 通过范畴实现装饰 (实例化)

- **why** ：

  1. 想要在不影响其他对象的情况下，以动态、透明的方式给单个对象添加职责
  2. 想要扩展一个类的行为，却做不到。类定义可能被隐藏，无法进行子类化；或者，对类的每个行为的扩展，为支持每种功能组合，将产生大量的子类
  3. 对类的职责的扩展是可选的

  <br>

  ---

  Tips

  - 真正子类方式的实现使用一种较为结构化的方式连接各种装饰器。范畴的方式更为简单和轻量，适用于现有类只需要少量装饰器的应用程序。虽然范畴不同于实际的子类化，不能严格实现模式的原始风格，但它实现了解决同样问题的意图。
  - cocoa中的装饰 [**Category**](https://www.raywenderlich.com/46988/ios-design-patterns) and [**Delegation**](https://www.raywenderlich.com/46988/ios-design-patterns).

  ---

  <br>

  <br>

  <img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>责任链</h3>

  - **what** : 

    使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间发生耦合。此模式将这些对象连城一条链，并沿着这条链传递请求，直到有一个对象处理它为止。

  - **how** ：

    通过传递请求的方式，形成责任链，每一次都传递和接收都做出相应处理

  - **why** ：

    1. 有多个对象可以处理请求，而处理程序只有在运行时才能确定
    2. 向一组对象发出请求，而不想显式指定处理请求的特定处理程序