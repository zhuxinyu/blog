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

     

     