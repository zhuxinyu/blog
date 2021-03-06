<h1>第三部分  接口适配</h1>

> 概要
>
> > - 适配器 adapter
> > - 桥接 bridge
> > - 外观

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>适配器</h3>

- **what** : 

  将一个类的接口转换成客户希望的另一个接口，适配器模式使得原来由于接口不兼容而不能一起工作的类可以一起工作

- **how** ：

   	1. 类适配器：通过多重继承实现
   	2. 对象适配器：通过协议 / Block 实现

- **why** ：

   	1. 已有类的接口与需求不匹配 ：平级适配
   	2. 想要一个可复用的类，该类能够同可能带有不兼容接口的其他类协作 ：父适配子
   	3. 需要适配一个父类的不同子类，可以让子类适配其父类 ：子适配父

<br>

---

Tips

Adaptee 被适配者 / Target 目标接口 / Adapter 适配器

|                       类适配器                        |                          对象适配器                          |
| :---------------------------------------------------: | :----------------------------------------------------------: |
|   只针对单一的具体Adaptee类，把Adaptee适配到Target    |                 可以适配多个Adaptee及其子类                  |
| 易于重载Adaptee的行为，因为是通过直接子类化进行的适配 | 难以重载Adaptee的行为，需要借助于子类的对象而不是Adaptee本身 |
|  只有一个Adapter对象，无须额外的指针间接访问Adaptee   |         需要额外的指针以间接访问Adaptee并适配其行为          |

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>桥接</h3>

- **what** : 

  将抽象部分与他的实现部分分离，使他们都可以独立的变化

- **how** ：

  通过对象组合将抽象与实现分离，双方互不影响

- **why** ：

  1. 不想在抽象与实现之间形成绑定关系，解耦
  2. 抽象及实现都可以通过子类化独立进行扩展
  3. 想在带有不同抽象接口的多个对象之间共享一个实现

<br>

---

Tips

​	AGAIN: 优先使用对象组合而不是继承

---

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>外观</h3>

- **what** : 

  为系统中的一组接口提供一个统一的接口。外观定义一个高层接口，让子系统更易于使用

- **how** ：

  将一组接口定义到一个高层接口中，调用这些子系统时可通过高层接口调用

- **why** ：

  1. 子系统正逐渐变得复杂，需要为子系统归档的时候
  2. 可对子系统进行分层，简化依赖关系