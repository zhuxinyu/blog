<h1>第九部分 对象状态</h1>

> 概要
>
> > - 备忘录 memento

<br>

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/logo.jpg" width = "30" height = "30" div align=left /><h3>备忘录</h3>

- **what** : 

  在不破坏封装的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可将该对象恢复到原先保存的状态。

- **how** ：

  此模式中有3个关键角色：原发器（originator）、备忘录（memento）和看管人（caretaker）。originator与caretaker交互memento， caretaker不与memento交互只负责保管和请求originator保存memento的状态。关键在于维持memento对象的私有性。memento类应该有两个接口：一个宽接口，给Originator用，一个窄接口，给其他对象用

- **why** ：

  1. 需要保存一个对象（或某部分）在某一时刻的状态，这样以后就可以恢复到先前的状态
  2. 用于获取状态的接口会暴露实现的细节，需要将其隐藏起来

<br>

---

Tips:

​	Cocoa Touch中的备忘录：归档 -> NSKeyedArchiver和NSKeyedUnarchiver

---

