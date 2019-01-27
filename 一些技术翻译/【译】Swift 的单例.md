# 【译】Swift 的单例

关于单例类 | 什么是单例模式

原文地址：https://medium.com/@nimjea/singleton-class-in-swift-17eef2d01d88



**单例**是一种在开发中非常流行的设计模式。大部分开发者都在用这种设计模式。这种模式非常简单，常见并且容易用在你的项目中。它用静态属性初始化你的class instance仅一次，并且全局的分享你的class instance。

我们用过很多次Apple's Foundation APIs 例如 **UserDefaults**.standard, **FileManager**.default.与单例类模式非常相似。

**这是一个简单的例子关于使用class**

```swift
class LocationManager{
//MARK: - Location Permission
    func requestForLocation(){
        //Code Process
        print("Location granted")
    }
    
}
//Access the class
let location = LocationManager() //initialization class
location.requestForLocation()    //Call function here 
```

这是一个没用单例模式的class，为了调用方法我们需要每次初始化class，为了避免这种情况我们使用带静态实例的单例类。

**写你的第一个单例class**

```swift
class LocationManager{
    
    static let shared = LocationManager()
    
    init(){}
    
    func requestForLocation(){
        //Code Process
        print("Location granted")
    }
    
}
//Access class function with Singleton Pattern 🚀
LocationManager.shared.requestForLocation()  //"Location granted"
//Still you can use your class like this
let location = LocationManager()
location.requestForLocation()
```

**写单例类更好的方式** 😎

```swift
class LocationManager{
    
    static let shared = LocationManager()
    
    var locationGranted: Bool?
    //Initializer access level change now
    private init(){}
    
    func requestForLocation(){
        //Code Process  
        locationGranted = true     
        print("Location granted")
    }
    
}
//Access class function in a single line
LocationManager.shared.requestForLocation()
```

修改入口初始化等级后你会得到这种错误 -

每个class有默认public的初始化器，它现在变成了private。现在你不再能初始化你的单例类。



**如何使用单例** 🎉

```swift
//In a single line you can access easily 
LocationManager.shared.requestForLocation() // "Location granted"
//Access variable value
print(LocationManager.shared.locationGranted ?? false) // true
```



**结论**

最后，你现在理解了如何创建**单例**类在你的项目中。创建非常省时。容易在项目中使用。他有一些**优缺点**，如果你用很多单例模式在项目中，很难管理单例的生命周期。而且，他维护**全局变量**的状态。尽量避免乱用**单例模式**，更多的使用**依赖注入**。👍🏻

**依赖注入**我会在下篇文章中谈到。😊

**感谢阅读** 🙌🏼

如果你有任何关于这篇教程的疑问？ 推我：[*@***Anand**](https://twitter.com/anand8402)

