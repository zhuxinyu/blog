# 【译】 siwft 4.2 代理模式

在swift中什么是代理协议 ? | 可选 和 必须的协议方法 ?

原文地址：https://medium.com/@nimjea/delegation-pattern-in-swift-4-2-f6aca61f4bf5

**什么是协议**

**根据**  [**Apple Documentation**](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)**-**

协议定义了适合特定任务或功能的方法、属性和其他需求的蓝图。协议可以被用在class, structure 或者 enumeration这些需求去提供一个实际的实现。任何满足协议需求的类型都被称作遵从协议。

除了指定符合类型必须实现的需求之外，你可以扩展一个协议来实现其中的一些需求，或者实现符合类型可以利用的其他功能。

在swift 语言中你看到过很多次协议，在开发基础表视图有**UITableViewDelegate & UITableViewDataSource**. 这两个协议都有他们自己的必需和可选的方法。如果你看过Apple的frameworks。

如果你按command键**(⌘)** 和鼠标左键点击**UITableViewDataSource** 你会看到这些选项-

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_Wo3GdtbO0GcnPOpxr_178g.png" width = "600" height = "225" div align=center />



现在点击**跳转到定义**，然后你会看到他们的协议方法 -

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_3IHuEk66pTf8YZq0t6D5zQ.png" width = "600" height = "225" div align=center />

这是一个例子关于Swift中的协议。现在看这是什么和如何创建我们自己的协议方法和如何在我们的项目中应用。



**如何创建你的协议？**

我们开始写协议但没有class，你会看到一些东西就像这样 -

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_5ENRKZvGDoFhcjWEOnjGSA.png" width = "600" height = "225" div align=center />

选择第一个选项或者按回车。之后，你会看起来像这样 - 

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_-qgQL--GCeInEnEjspuS6g.png" width = "600" height = "225" div align=center />

现在写你的协议名称和需求，用你想要的方法和变量。我创建了一个名字叫DeveloperEntryDelegate的协议，我在这用的是AnyObject 因为如果你想使用它就让它变成弱引用，否则就忽略它。

**协议声明**

```swift
protocol DeveloperEntryDelegate{
    func textDeveloperPlatform(_ text: String)
    func textDeveloperLanguage(_ text: String)
}
```

**在class中应用**

```swift
weak var delegate: DeveloperEntryDelegate?
```

你会看到下面的错误关于弱引用协议声明 - 

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_kOf8zpOFO9sdusDdaD4CuQ.png" width = "600" height = "225" div align=center />

现在用协议的类型**AnyObject**修复这个错误

```swift
protocol DeveloperEntryDelegate: AnyObject {
    func textDeveloperPlatform(_ text: String)
    func textDeveloperLanguage(_ text: String)
}
```

现在看你的class， 我们要在那里声明它

<img src="https://github.com/zhuxinyu/blog/blob/master/%E4%B8%80%E4%BA%9B%E6%8A%80%E6%9C%AF%E7%BF%BB%E8%AF%91/1_G86cJWi52_y0iuQSBwO4GQ.png" width = "600" height = "225" div align=center />

**现在看他如何工作**

【此处应有视频】

https://youtu.be/SO1Gj7YA48c

本质上我们用的代理是为了回调传值或者方法从一个发起者class到另一个class。这会1v1进行交流。

在这个例子中，我们尅看到从第一个视图到第二个视图导航和写在textfields。再secondViewController点击Done按钮之后，代理方法传回FirstViewController的文本数据通过DeveloperEntryDelegate协议方法。这非常有用当你想要做一些改变从一个视图到另一个视图。非常易用。你可以找到这个例子在🐔ithub上~[**Github**](https://github.com/ANSCoder/Delegation-Example)。

**FistViewController** 内部 -

```swift
class FirstViewController: UIViewController {
      @IBOutlet weak var labelPlatformDetails: UILabel!
      @IBOutlet weak var labelDeveloperLanguage: UILabel!
override func viewDidLoad() {
    super.viewDidLoad()
}
//MARK: - Navigation
@IBAction func actionAddDetail(_ sender: UIButton) {
   guard  let secondView = self.storyboard?.instantiateViewController(withIdentifier: "SecondViewController") as? SecondViewController else {   
       fatalError("View Controller not found")}
secondView.delegate = self //Protocol conformation here
navigationController?.pushViewController(secondView, animated: true)}
}
//MARK: - Protocol Delegate Methods
extension FirstViewController: DeveloperEntryDelegate {
   func textDeveloperPlatform(_ text: String){
      labelPlatformDetails.text = "Platform: \(text)" }
func textDeveloperLanguage(_ text: String) {
    labelDeveloperLanguage.text = "Language: \(text)" } 
}
```

**SecondViewController** 内部 -

```swift
protocol DeveloperEntryDelegate: AnyObject {
func textDeveloperPlatform(_ text: String)
func textDeveloperLanguage(_ text: String) }
class SecondViewController: UIViewController {
      weak var delegate: DeveloperEntryDelegate?
      @IBOutlet weak var textPlateform: UITextField!
      @IBOutlet weak var textLanguage: UITextField!
override func viewDidLoad() {
         super.viewDidLoad() }
  //MARK: - Action Pass back view Details
  @IBAction func actionDone(_ sender: UIButton) {
    self.navigationController?.popViewController(animated: true)
    self.delegate?.textDeveloperPlatform(textPlateform.text ?? "")
    self.delegate?.textDeveloperLanguage(textLanguage.text ?? "")
   }
}
```



**如何实现可选协议方法**

通过添加@objc在你的协议和**@objc optional method**做到。👍🏽

```swift
@objc protocol DeveloperEntryDelegate: AnyObject {
   func textDeveloperPlatform(_ text: String)
   @objc optional func textDeveloperLanguage(_ text: String)
}
```

如果你想要用另一个方式实现协议的可选方法。你必须对你的**可选协议方法**创建extension。😎 🎉

```swift
protocol DeveloperEntryDelegate: AnyObject {
    func textDeveloperPlatform(_ text: String)
    func textDeveloperLanguage(_ text: String) //optional method
}
//optional method
extension DeveloperEntryDelegate {
   func textDeveloperLanguage(_ text: String){}
}

```

**结论**

协议代理模式是Apple的框架中一个非常重要的部分，你的编程中可以让一个class和另一个class交流变得简单。我看到过一些开发者出事步骤没有人知道如何传值从一个视图到另一个视图，所以他们视图解决这个问题通过用UserDefaults或者全局变量来本地存值。顺便说一下如果你有任何本地储存功能但不再获取他，这不是正确的选择。所以代理或者更简单更快。🎉

在这一部分，我们知道了什么是协议。如何创建它和如何用代理模式工作。在那之后你也懂了可选和必需协议方法。默认情况下，方法是必须的。如果你想要让它更灵活你可以让他变成可选方法。我希望你享受它。😊✌🏼



**感谢阅读** 🙌🏼

如果你有任何疑问关于这篇教程？ | 如果你认为你能做到更简单的方法或者更少额外的事关于这个东西请让我知道，私信或者评论 - 推~[**Twitter**](https://twitter.com/anand8402)