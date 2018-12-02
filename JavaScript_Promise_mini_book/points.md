<h1>JavaScript Promise迷你书</h1>

- Promise是抽象异步处理对象以及对其进行各种操作的组件

- 最初被提出是在基于并列/并行处理设计的E语言中

- 异步处理对象和处理规则规范化，并按照统一的接口来编写，采取规定方法之外的写法都会出错，将复杂的异步处理轻松地进行模式化是使用promsie的理由之一

- 在ES6标准中定义的三种API类型:

   	1. Constructor：可以使用new来调用promise的构造器进行实例化
   	2. Instance Method: promise对象的回调方式promise.then(onFulfilled, onRejected) 成功失败都可以使用,成功调用onFulfilled，失败调用onRejected,有catch时失败会优先进入catch
   	3. Static Method: 例如`promise.all()`,` promise.resolve()`等一些静态方法，主要都是对promise进行操作的辅助方法

- workflow的方式形成method chain：`(promise instance).then((success, error) => {return}).catch(err)`
- promise instance的三种状态：<img src="https://github.com/zhuxinyu/blog/blob/master/JavaScript_Promise_mini_book/promise-onFulfilled_onRejected.png" width = "310" height = "170" div align=right />

   1. has-resolution - fulfilled (成功)
   2. has-rejection - rejected (失败)
   3. unresolved - pending (进行中，未回调)
- promise与event等不同，回调方法只会执行一次
- 静态方法`Promise.resolve(value)` 可以认为是 `new Promise()` 方法的快捷方式
- `Promise.resolve` 方法另一个作用就是将 [thenable](http://liubin.org/promises-book/#Thenable) 对象转换为promise对象，要求thenable对象所拥有的 `then` 方法应该和Promise所拥有的 `then` 方法具有**同样的功能和处理过程**。
- js中的异步运行机制：同步任务在主线程执行，并形成任务栈**（execution context stack**，异步任务在任务队列**(task queue)**中执行, 一旦没有同步任务执行时就从任务队列中读取异步任务执行，有同步任务时就在主线程结束当前任务后开始执行。
- setTimeout 和 setInterval 是典型的异步调用
- **不要对异步回调函数进行同步调用**处理顺序可能会与预期不符，可能带来意料之外的后果，还可能导致栈溢出或异常处理错乱等问题，如果想在将来某时刻调用异步回调函数的话，可以使用 `setTimeout` 等异步API
- throw 会截断 promise chain 的workflow ，提前结束promise chain
- `Promise.then()` 不仅仅是注册一个回调函数那么简单，它还会将回调函数的返回值进行变换，创建并返回一个promise对象。

