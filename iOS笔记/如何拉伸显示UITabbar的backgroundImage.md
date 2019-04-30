## 如何拉伸显示UITabbar的backgroundImage

努力找个blog写 没找到啥喜欢的平台 想去sina还维护半个月😂 先借用github凑合一下 我知道这不合规矩 以后再移走

遇到个问题记录一下： UITabbar的backgroundImage默认平铺显示，我试图让它拉伸显示

<br>

一开始我试图查下[文档](<https://developer.apple.com/documentation/uikit/uitabbar/1623469-backgroundimage>)和[Stack Overflow](<https://stackoverflow.com/questions/42287662/how-to-change-the-background-image-of-tab-bar-in-objective-c>): 如果你想拉伸看下[UIImage.Resizing](<https://developer.apple.com/documentation/uikit/uiimage/resizingmode>)。👌 看起来很容易

```swift
let img = UIImage(named: "backgroundTabbar")?.resizableImage(withCapInsets: .zero, resizingMode: .stretch)
homeVC?.tabBar.backgroundImage = img
```

<img src="https://github.com/zhuxinyu/blog/blob/master/iOS%E7%AC%94%E8%AE%B0/WX20190429-212418%402x.png" width = "716" height = "258" div align=center />

看起来并不ok🤔 试了多种参数都不行 受不了 咱直接看看他到底啥意思

<br>

```swift
/* The background image will be tiled to fit, even if it was not created via the UIImage resizableImage methods.
     */
    @available(iOS 5.0, *)
    open var backgroundImage: UIImage?
```

好的 注释说了 就是平铺，你想咋的？ resizableImage也不行🙃

<br>

不让就不让 也行 至少知道问题出在哪了 继续google 找一个[11年的帖子](<https://stackoverflow.com/questions/8517751/how-to-stretch-backgroundimage-in-uinavigationbar-and-uitabbar-when-autoresized>) 说用`stretchableImage(withLeftCapWidth:topCapHeight:)`这个能解决 抱着~~死马当活马医~~实践是检验真理唯一标准的心态试了一下 还真成了！

<br>

<img src="https://github.com/zhuxinyu/blog/blob/master/iOS%E7%AC%94%E8%AE%B0/WX20190429-210445%402x.png" width = "842" height = "202" div align=center />

<br>

> Creates and returns a new image object with the specified cap values.
>
> Deprecated
>
> Deprecated. Use the [`resizableImage(withCapInsets:)`](https://developer.apple.com/documentation/uikit/uiimage/1624102-resizableimage) instead, specifying cap insets such that the interior is a `1x1` area.

<br>

[文档](<https://developer.apple.com/documentation/uikit/uiimage/1624145-stretchableimage>)看了一眼 ，这个处理图片的方法iOS5被弃用了，但我在iOS12用完全不报警。。咱也不知道 咱也不敢问😂 以上

