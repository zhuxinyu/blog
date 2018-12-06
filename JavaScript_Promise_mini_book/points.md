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

- js中的异步运行机制：同步任务在主线程执行，并形成任务栈**(execution context stack)** ，异步任务在任务队列**(task queue)**中执行, 一旦没有同步任务执行时就从任务队列中读取异步任务执行，有同步任务时就在主线程结束当前任务后开始执行。

- setTimeout 和 setInterval 是典型的异步调用

- **不要对异步回调函数进行同步调用**处理顺序可能会与预期不符，可能带来意料之外的后果，还可能导致栈溢出或异常处理错乱等问题，如果想在将来某时刻调用异步回调函数的话，可以使用 `setTimeout` 等异步API

- throw 会截断 promise chain 的workflow ，提前结束promise chain

- `Promise.then()` 不仅仅是注册一个回调函数那么简单，它还会将回调函数的返回值进行变换，创建并返回一个promise对象。

- 实际上 `Promise.catch`只是 `promise.then(undefined, onRejected);` 方法的一个别名而已。 也就是说，这个方法用来注册当promise对象状态变为Rejected时的回调函数。

- [点标记法（dot notation）](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Property_Accessors#Dot_notation) 要求对象的属性必须是有效的标识符（在ECMAScript 3中则不能使用保留字），

   但是使用 [中括号标记法（bracket notation）](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Property_Accessors#Bracket_notation)的话，则可以将非合法标识符作为对象的属性名使用,解决Promise#catch标识符冲突问题 (IE8 以下都是ES3)

- **每次调用then都会返回一个新创建的promise对象**

- `Promise.all`的promise数组是同时开始执行的, 也就是并行处理模式。

- `Promise.race` 只要有一个promise对象进入 FulFilled 或者 Rejected 状态的话，就会执行then处理后续工作，且不会取消其他promise对象，会继续执行完。

- 处理错误：遵循then catch flow

- 如果说一个类库具有 `then` 兼容性的话，实际上指的是 [Thenable](http://liubin.org/promises-book/#Thenable) ，它通过使用 [Promise.resolve](http://liubin.org/promises-book/#Promise.resolve) 基于ES6 Promise的规定，进行promise对象的变换。

- [jakearchibald/es6-promise](https://github.com/jakearchibald/es6-promise) 一个兼容 ES6 Promises 的Polyfill类库。 它基于 [RSVP.js](https://github.com/tildeio/rsvp.js) 这个兼容 Promises/A+ 的类库， 它只是 RSVP.js 的一个子集，只实现了Promises 规定的 API。

- [yahoo/ypromise](https://github.com/yahoo/ypromise) 这是一个独立版本的 [YUI](http://yuilibrary.com/) 的 Promise Polyfill，具有和 ES6 Promises 的兼容性。 本书的示例代码也都是基于这个 ypromise 的 Polyfill 来在线运行的。

- [getify/native-promise-only](https://github.com/getify/native-promise-only/) 以作为ES6 Promises的polyfill为目的的类库 它严格按照ES6 Promises的规范设计，没有添加在规范中没有定义的功能。 如果运行环境有原生的Promise支持的话，则优先使用原生的Promise支持。

- [kriskowal/q](https://github.com/kriskowal/q) 类库 `Q` 实现了 Promises 和 Deferreds 等规范。 它自2009年开始开发，还提供了面向Node.js的文件IO API [Q-IO](https://github.com/kriskowal/q-io) 等， 是一个在很多场景下都能用得到的类库。（ [API Reference · kriskowal/q Wiki](https://github.com/kriskowal/q/wiki/API-Reference)）

- [petkaantonov/bluebird](https://github.com/petkaantonov/bluebird) 这个类库除了兼容 Promise 规范之外，还扩展了取消promise对象的运行，取得promise的运行进度，以及错误处理的扩展检测等非常丰富的功能，此外它在实现上还在性能问题下了很大的功夫（[bluebird/API.md at master · petkaantonov/bluebird](https://github.com/petkaantonov/bluebird/blob/master/API.md))

- 如果在Promise中使用 `throw` 语句的话，会被 `try...catch` 住，最终promise对象也变为Rejected状态。

- 如果想把 [promise对象状态](http://liubin.org/promises-book/#promise-states) 设置为Rejected状态的话，使用 `reject` 方法则更显得合理。

- 看到此图应该就很容易理解了，Deferred和Promise并不是处于竞争的关系，<img src="https://github.com/zhuxinyu/blog/blob/master/JavaScript_Promise_mini_book/deferred-and-promise.png" width = "180" height = "300" div align=right />

   而是Deferred内涵了Promise。

- 如果说Promise是用来对值进行抽象的话，Deferred则是对处理还没有结束的状态或操作进行抽象化的对象.

- 用`promise.rice`的特性实现超时判断，两个对象竞速，其中一个任务的延迟定义为超时标准时间，若此任务优先完成，即判定为超时并throw错误。

- 通过模块化实现promise对象和操作的分离

- Promise能非常灵活的进行处理流程的控制，为了充分发挥它的能力，我们需要注意不要将一个函数写的过于庞大冗长，而是应该将其分割成更小更简单的处理，并对JavaScript中提到的机制进行更深入的了解。

- `then`和`done`的区别

   - `done` 并不返回promise对象
     - 也就是说，在done之后不能使用 `catch` 等方法组成方法链
   - `done` 中发生的异常会被直接抛给外面
     - 也就是说，不会进行Promise的错误处理（Error Handling）

- 原生promise ：错误被内部消化的问题也被称为 *unhandled rejection* ，从字面上看就是在Rejected时没有找到相应处理的意思。

   |      | 这种unhandled rejection错误到底有多难检查，也依赖于Promise的实现。 比如 [ypromise](https://github.com/yahoo/ypromise) 在检测到 unhandled rejection 错误的时候，会在控制台上提示相应的信息。Promise rejected but no error handlers were registered to it另外， [Bluebird](https://github.com/petkaantonov/bluebird) 在比较明显的人为错误，即ReferenceError等错误的时候，会直接显示到控制台上。"Possibly unhandled ReferenceError. conosle is not defined原生（Native）的 Promise实现为了应对同样问题，提供了GC-based unhandled rejection tracking功能。该功能是在promise对象被垃圾回收器回收的时候，如果是unhandled rejection的话，则进行错误显示的一种机制。[Firefox](https://twitter.com/domenic/status/461154989856264192) 或 [Chrome](https://code.google.com/p/v8/issues/detail?id=3093) 的原生Promise都进行了部分实现。 |
   | ---- | ------------------------------------------------------------ |

- 在Promise中，我们可以选择多种方法来实现处理的按顺序执行。

   - [循环使用then调用的方法](http://liubin.org/promises-book/#multiple-xhr.js)
   - [使用for循环的方法](http://liubin.org/promises-book/#promise-foreach-xhr.js)
   - [使用reduce的方法](http://liubin.org/promises-book/#promise-reduce-xhr.js)
   - [分离出顺序处理函数的方法](http://liubin.org/promises-book/#promise-sequence.js)

---

END. [原文地址](http://liubin.org/promises-book/#introduction)