# UI视图

不知道是不是原作者，blog答案很详细~ 

[UI - 1](https://l-vincent.github.io/2018/05/08/%E9%9D%A2%E8%AF%95-UI%E5%89%96%E6%9E%90/) [UI - 2](https://l-vincent.github.io/2018/05/10/%E9%9D%A2%E8%AF%95-UI%E5%89%96%E6%9E%90(%E4%BA%8C)/)

### UITableview相关：

- **重用机制**(对象池设计模式)：复用池 (初始空,队列或者链表) -> 根据reuseIdentifier（具有不可变性）获取cell （复用池内cell个数小于tableview显示个数时生成新的cell）-> 每次取出会重置[cell](https://developer.apple.com/documentation/uikit/uitableviewcell/1623223-prepareforreuse)的content

  

  [UITableViewCell复用机制](https://www.jianshu.com/p/1046c741fce1)

  [对象池设计模式](https://en.wikipedia.org/wiki/Creational_pattern)

  [UITableViewCell Apple Doc](https://developer.apple.com/documentation/uikit/uitableviewcell#//apple_ref/occ/instp/UITableViewCell/reuseIdentifier)

  [UICollectionViewCell重用的写法](https://stackoverflow.com/questions/22320487/uicollectionviewcell-reuse)

  [UITableViewCell重用的写法](https://stackoverflow.com/questions/9117211/what-if-no-reusable-cell-in-uitableview)

  <br>

- **数据源同步**：主线程更新UI，异步更新其他数据及异步下载缓存数据。

  [数据源同步更新tableview的synchronized问题](https://stackoverflow.com/questions/13280820/uitableviewdatasource-and-multithreading)

  [ASIHTTPReques+GCD](https://www.raywenderlich.com/3049-multithreading-and-grand-central-dispatch-on-ios-for-beginners-tutorial)

  [CachingAnything in iOS(🤣 i love the title)](https://medium.com/ios-os-x-development/caching-anything-in-ios-102176e46eba)

  [Protocol Oriented Programming is Not a Silver Bullet]( http://chris.eidhof.nl/post/protocol-oriented-programming/)

  [Updating UI From Background Threads, Simple Threading In Swift 3 For IOS](https://www.electrollama.net/blog/2017/1/6/updating-ui-from-background-threads-simple-threading-in-swift-3-for-ios)

### 事件传递&视图响应：

- **事件传递**:
  1. if (!hidden &$ userInteractionEnable && alpha > 0.01) { next }  else { return nil }
  2. 判断点击的点是否在当前范围内，为YES直接下一步. 不在则直接返回nil
  3. 倒序遍历所有子视图，同时调用 hitTest 方法，如果某个子视图返回了对应的响应视图，这个响应视图会返回给响应方，如果遍历完都返回nil，就返回当前点击位置在当前视图范围内的视图作为响应视图。

```swift
UIApplication -> UIWindow -> hitTest:withEvent:
```

- 视图响应链：（个人理解）
  1. 与传递链相反
  2. 且只有点击位置在视图内的才会参与响应链
  3. 到 UIApplicationDelegate 依然没有任何视图处理该事件的时候，直接忽略此事件， 并不会崩溃。

- UIView和CALayer:

  1. UIView为CALayer提供内容，以及负责处理触摸等事件，参与响应链。

  2. CALayer负责显示内容contents

  3. 设计概念：[单一职责](https://blog.csdn.net/zhengzhb/article/details/7278174)

     ~ 扩展阅读：设计模式六大原则：[单一职责](https://blog.csdn.net/zhengzhb/article/details/7278174)、[里式替换](https://blog.csdn.net/zhengzhb/article/details/7281833)、[依赖倒置](https://blog.csdn.net/zhengzhb/article/details/7289269)、[接口隔离](https://blog.csdn.net/zhengzhb/article/details/7296921)、[迪米特](https://blog.csdn.net/zhengzhb/article/details/7296930)、[开闭原则](https://blog.csdn.net/zhengzhb/article/details/7296944)

### 图像显示原理：

- CPU的工作：
  1. UI布局
  2. 文本计算
  3. 绘制，比如drawRect方法
  4. 图片编解码
  5. 提交位图
- CPU渲染管线：
  1. 文理渲染
  2. 视图混合

### 卡顿 & 掉帧：

- UI卡顿、掉帧的原因：
  1. 页面滑动流畅性是60fps，也就是16.7ms一个vsync信号刷新一次，CPU 花费时间绘图解码之后将位图交给 GPU 合成渲染产生一帧画面。
  2. CPU解码和GPU渲染的时间超过了16.7毫秒就会出现掉帧，显示效果就是卡顿啦。

### UITableView 的滑动优化方案：

- CPU: (CoreGraphics)

  1. 对象创建、调整、销毁

  2. 预排版（布局计算，文本计算）

  3. 预渲染 （文本异步绘制， 图片编解码等）

     像对象创建，布局计算等都可以放到子线程去做，主线程可以有更多的时间去响应用户的交互

- GPU: (QuartzCore) 接收提交的纹理（Texture）和顶点描述（三角形），应用变换（transform）、混合并渲染，然后输出到屏幕上

  1. 文理渲染：避免[离屏渲染](https://www.jianshu.com/p/6d24a4c29e18)

  2. 视图混合：视图层叠需要进行像素计算，可降低视图复杂度，通过CPU层面的异步绘制（例如drawRect），达到提交的位图本身就是一个层级少的视图。 （coretext绘制）

     扩展阅读：

     - [iOS开发：UITableView的优化技巧－异步绘制Cell](https://blog.csdn.net/mo_xiao_mo/article/details/52622172)

     - [基于 CoreText 的排版引擎：基础](https://blog.devtang.com/2015/06/27/using-coretext-1/)

       **NS_ASSUME_NONNULL_BEGIN && NS_ASSUME_NONNULL_END**

     - [Object-C中的黑魔法](https://www.jianshu.com/p/b3a31eed945f)

     - [NS_ASSUME_NONNULL_BEGIN和NS_ASSUME_NONNULL_END](https://www.jianshu.com/p/67aa3bbb68c6)

       **__kindof**

     - [Xcode 7新的特性Lightweight Generics 轻量级泛型与__kindof修饰符](https://blog.csdn.net/leikezhu1981/article/details/47418011)

       **CFRELEASE**

     - [Objective-C 和 Core Foundation 对象相互转换的内存管理总结](https://blog.csdn.net/yiyaaixuexi/article/details/8553659)

     - [Objective-CObjective-C的"多继承"](https://blog.csdn.net/yiyaaixuexi/article/details/8970734)

     - [iOS安全攻防（十七）：Fishhook](https://blog.csdn.net/yiyaaixuexi/article/details/19094765)

       

       

