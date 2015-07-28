---
layout: post
title: Optional in Swift
---
###为什么要有Optional

一项新技术的出现肯定是有其背景原因。作为程序员我们希望尽早发现我们代码中的问题。能在编译器阶段发现的，就不在运行时阶段发现。

看下面Objective-C代码:

{% highlight objective-c linenos=table %}
NSString *message = @"Objective-C will never die!";
message = nil;
NSLog(message.isEmpty) // 运行时出错
{% endhighlight %}

如何能在编译器就发现这个问题呢，Optional出场了。我们看下Swift代码。

{% highlight swift linenos=table %}
// 表示message是一个optional对象，message的值可能为nil，也可能是一个字符串。
var message:String? = "Swift will find out the error!"
// message可以赋值nil
message = nil
// 编译错误, message为Optional对象，不能直接取isEmpty值。需要进行unwrapped操作，同事也给程序员一个机会确认自己代码的正确性
println(message.isEmpty)
{% endhighlight %}

如何处理这个编译错误？两种方式。

第一种
{% highlight swift linenos=table %}
// 程序员主动确认message不可能为空。如果message为nil，则运行时错误；如果message有值，则返回对应的值。
println(message!.isEmpty) 
{% endhighlight %}

第二种
{% highlight swift linenos=table %}
// 程序员主动确认message有可能为空。如果message为nil，则返回nil；如果message有值，则为返回Optional对象，包裹的是对应的值。
println(message?.isEmpty) 
{% endhighlight %}

Optional的出现就是为了让程序员更早的在编译器发现问题，然后进行及时的确认。

###Optional语法

####Optional的声明
{% highlight swift linenos=table %}
// 声明str为一个Optional String类型。str有可能是nil，有可能是一个字符串。
var str:String? = "I am a string"
{% endhighlight %}

####Optional的unwrapped操作
Optional里面包了一个值，如果不为nil，要取里面的值，则需要unwrapped操作。
{% highlight swift linenos=table %}
// 隐试的unwrapped。如果str为nil，则不进入if语句；如果有值，则unwrappedStr为optional包含的值。
if unwrappedStr = str{
    println(unwrappedStr)    
}
{% endhighlight %}

{% highlight swift linenos=table %}
// 显示的unwrapped
println(str!)
{% endhighlight %}

#### Optional中的?和!
{% highlight swift linenos=table %}
var str:String? = "I am a string"
// 必须unwrapped，然后才能引用到值。
println(str!)

// String!表示也是Optional类型，但是表示隐式的unwrapped，所以可以直接引用对应值。
var str:String! = "I am a string"
println(str)
{% endhighlight %}


###Optional源码
{% highlight swift linenos=table %}
enum Optional<T> : Reflectable, NilLiteralConvertible {
    case None
    case Some(T)

    /// Construct a `nil` instance.
    init()

    /// Construct a non-\ `nil` instance that stores `some`.
    init(_ some: T)

    /// If `self == nil`, returns `nil`.  Otherwise, returns `f(self!)`.
    func map<U>(f: @noescape (T) -> U) -> U?

    /// Returns `f(self)!` iff `self` and `f(self)` are not nil.
    func flatMap<U>(f: @noescape (T) -> U?) -> U?

    /// Returns a mirror that reflects `self`.
    func getMirror() -> MirrorType

    /// Create an instance initialized with `nil`.
    init(nilLiteral: ())
}
{% endhighlight %}
从声明上看，Optional其实是一个模板enum。从继承关系来看，它可以反射，可以被设置成nil。有两种值，一种是None(nil)，一种是有模板参数类型的值。


###Reference

[Optional Type in Swift for beginners](http://www.appcoda.com/beginners-guide-optionals-swift/)