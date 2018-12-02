<h1>JavaScript Promise迷你书</h1>

- Promise是抽象异步处理对象以及对其进行各种操作的组件
- 最初被提出是在基于并列/并行处理设计的E语言中
- 异步处理对象和处理规则规范化，并按照统一的接口来编写，采取规定方法之外的写法都会出错，将复杂的异步处理轻松地进行模式化是使用promsie的理由之一
- 在ES6标准中定义的三种API类型:
   	1. Constructor：可以使用new来调用promise的构造器进行实例化
   	2. Instance Method: promise对象的回调方式promise.then(onFulfilled, onRejected) 成功失败都可以使用,成功调用onFulfilled，失败调用onRejected,有catch时失败会优先进入catch
   	3. Static Method: 例如promise.all(), promise.resolve()等一些静态方法，主要都是对promise进行操作的辅助方法
- workflow的方式：(promise instance).then((success, error) => {return}).catch(err)
- promise instance的三种状态：
   	1. has-resolution - fulfilled (成功)
   	2. has-rejection - rejected (失败)
   	3. unresolved - pending (既不是成功也不是失败，是promise instance被创建后的初始化状态, 或者说是进行中，未回调)

<img src="https://github.com/zhuxinyu/blog/blob/master/JavaScript_Promise_mini_book/WeChat5a1ab298e01829dd4b3fdea1b5fdcea4.png" width = "310" height = "170" div align=left />

- Promise与Event等不同，在回调函数执行的函数只会被调用一次