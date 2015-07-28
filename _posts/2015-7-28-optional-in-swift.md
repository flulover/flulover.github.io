---
layout: post
title: Swift简介
---
Swift是苹果平台的新语言，语法比Object-C更加简化，开发效率也会更高。这两天快速学习了下Swift，用XCode的PlayGround写了两个小程序，分别关于基本数据类型和面向对象的部分。

* [Swift Basic](https://github.com/flulover/LearnSwift/blob/master/Basic.playground/section-1.swift)
* [Swift OO](https://github.com/flulover/LearnSwift/blob/master/SwiftOO.playground/section-1.swift)

下面详细列出一些比较有意思的地方：

1.

{% highlight swift %}
let i = 1; // 常量 i += 1; 会报错
var i = 1; // 变量
{% endhighlight %}

2.
{% highlight swift %}
let i = 1; // 编译器可以自动推断出类型
let i:Integer = 1; // 也可以显示指定
{% endhighlight %}

3.
{% highlight swift %}
let names:[String] = ["Ted","YuanZheng", "Other name"]; // 数组（显示）
for name in names {
    println(name);
}
{% endhighlight %}

4.
{% highlight swift %}
let persons = ["Ted": 18, "YuanZheng": 29, "Other Name": 100]; // 字典对象
for (name, age) in persons {
    println("\(name):\(age)");
{% endhighlight %}


5.
{% highlight Objective-C %}
if is_log_open { // 不需要空格
    println("Log is opened");
}
{% endhighlight %}

6.
{% highlight Objective-C  %}
for index in 1...5 { // 范围用...表示
    println(index);
}
{% endhighlight %}

7.

{% highlight Objective-C %}
let option = 2;
switch option{
case 1, 2: // 多个选择，不需要break，默认自动跳出switch
    println("Option is 1 or 2");
    // Do not need break here
case 3:
    println("Option is 3");
default:
    println("Option is default");
}
{% endhighlight %}

8.

{% highlight Objective-C %}
class Person
{
    let name: String;
    let age: Int;

    init(){ // 构造函数名字指定为init
        name = "Ted";
        age = 29;
    }

    init(name:String, age:Int){ // Paramater declaration is still the old way, this is suck!
        self.name = name;
        self.age = age;
    }


    func dump(){ // func is the function keywork
        println(fullName());
    }

    func fullName() -> String { // Stupid Swift, what about "String fullName()". Maybe the Swift designer want to keep the consistent with
        return "\(name):\(age)";
    }
}


let yzzhou = Person(name:"Yzzhou", age:29); // This is stupid, why I need to specify. But it dosen't need new keywork.
yzzhou.dump();
{% endhighlight %}

