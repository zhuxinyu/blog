# UI视图

### UITableview相关：

- **重用机制**(对象池设计模式)：复用池 (初始空,队列或者链表) -> 根据reuseIdentifier（具有不可变性）获取cell （复用池内cell个数小于tableview显示个数时生成新的cell）-> 每次取出会重置cell的content (https://developer.apple.com/documentation/uikit/uitableviewcell/1623223-prepareforreuse)

  

  UITableViewCell复用机制：https://www.jianshu.com/p/1046c741fce1

  对象池设计模式：https://en.wikipedia.org/wiki/Creational_pattern

  UITableViewCell Apple Doc: https://developer.apple.com/documentation/uikit/uitableviewcell#//apple_ref/occ/instp/UITableViewCell/reuseIdentifier

  UICollectionViewCell重用的写法：https://stackoverflow.com/questions/22320487/uicollectionviewcell-reuse

  UITableViewCell重用的写法: https://stackoverflow.com/questions/9117211/what-if-no-reusable-cell-in-uitableview

  <br>

- **数据源同步**：主线程更新UI，异步更新其他数据及异步下载缓存数据。

  数据源同步更新tableview的synchronized问题：https://stackoverflow.com/questions/13280820/uitableviewdatasource-and-multithreading

  ASIHTTPReques+GCD：https://www.raywenderlich.com/3049-multithreading-and-grand-central-dispatch-on-ios-for-beginners-tutorial

  CachingAnything in iOS(🤣 i love the title):https://medium.com/ios-os-x-development/caching-anything-in-ios-102176e46eba

  Protocol Oriented Programming is Not a Silver Bullet: http://chris.eidhof.nl/post/protocol-oriented-programming/

  Updating UI From Background Threads, Simple Threading In Swift 3 For IOS: https://www.electrollama.net/blog/2017/1/6/updating-ui-from-background-threads-simple-threading-in-swift-3-for-ios

