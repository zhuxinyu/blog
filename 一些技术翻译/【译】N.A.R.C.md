# 【译】**N.A.R.C**

原文链接：http://vgable.com/blog/tag/autorelease/

如何记住Cocoa内存管理：

> 想一下 **NARC**: "New Alloc Retain Copy". 如果你不做任何这些事，就不需要release。

-Andiih [on Stack Overflow](https://stackoverflow.com/questions/2865185/do-you-need-to-release-parameters-of-methods-at-the-end-of-them-in-objective-c)

个人见解， 我喜欢立即释放autorelease任何我NARC的东西，在同一条线上。例如：

```objective-c
Foo* pityTheFoo = [[[Foo alloc] init] autorelease];
```

不可否认，这样会造成一些难看的、泛白的线条。但我认为这值得，因为你不在需要担心关于release。

**用@property(或者 Setter) 替代 retain**

换句话说我喜欢这样写init方法：

```objective-c
- (id) init
{
	self = [super init];
	if (self) {
		_ivar = [[Foo alloc] init];
	}
	return self;
}
```

as:

```objective-c
- (id) init
{
	self = [super init];
	if (self) {
		self._ivar = [[[Foo alloc] init] autorelease];
	}
	return self;
}
```

(或者  `[self setIvar:[[[Foo alloc] init] autorelease]];` 如果你是讨厌点语法的人)

是否[在init和dealloc中使用acessors](https://www.mikeash.com/pyblog/friday-qa-2009-11-27-using-accessors-in-init-and-dealloc.html)是一个好主意，这是有争议的。我甚至留言在那篇争论中反对这一点。但从那以后，我做了很多反思，根据我的经验，使用@property而不是显式的release/= nil可以解决更多的问题。所以我认为这是最好的实践。

即使您不同意我的观点，如果您**显式地NARC对象的惟一位置是init、dealloc和setX: methods**，那么我认为您做的是正确的。

**环！**

内存管理难题的最后一块是[retian 环](https://www.mikeash.com/pyblog/friday-qa-2010-04-30-dealing-with-retain-cycles.html)。到目前为止，我所看到的关于他们最好的建议是[Mike Ash的文章](http://www.mikeash.com/pyblog/friday-qa-2010-04-30-dealing-with-retain-cycles.html)。阅读它。

---

# **如何写Cocoa对象的Getters**

Setters 比 getters 更直观简单，因为你不需要关心内存管理。

最好的实现是让编译器给你写getter，通过用[声明属性](http://developer.apple.com/documentation/Cocoa/Conceptual/ObjectiveC/Articles/ocProperties.html)

但是当你不得不手动实现getter时，我推荐（据我所知）安全模式，

```objective-c
- (TypeOfX*) x;
{
  return [[x retain] autorelease];
}
```

注意，根据Objective-C中的约定，变量jabberwocky的getter被简单地称为jabberwocky，而不是getJabberwocky。（译者：getter的命名规则）

# **为什么retain后要autorelease**

基本上 `return [[x retain] autorelease];`确保getter返回的内容在调用getter的代码中的任何本地对象中都是有效的。

考虑，

```objective-c
NSString* oldName = [person name];
[person setName:@"Alice"];
NSLog(@"%@ has changed their name to Alice", oldName);
```

如果`-setName:` 立即 `release` 值, 返回  `-name`, `oldName` 会在`NSLog`中无效。 

（未完待续）

