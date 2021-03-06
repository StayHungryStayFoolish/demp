---
layout:     post
title:      "Java 访问限定修饰符 "
subtitle:   "拒绝共享"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-13
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 修饰类
    - 修饰方法
    - static
    - abstract
    - final
---

## 什么是访问限定修饰符？

    - 比如你，有一个女朋友，还有一些朋友，我就是你其中一个好基友。我们关系很好，

      可是你的女朋友是属于你自己的，她不是我的。但是呀，你的朋友或许会变成我的朋友。

      你还有父母，还会有后代。

      这些都是你自己的，你不会给我，我也不要，我唯一要的就是你的女朋友。

      可这个时候，你用 private （私有的） 来修饰了，加了限定，别人都接触不到了。

      于是访问限定修饰符就有了，继承也有了。

      万物皆对象，你就是一个对象。

      你的女朋友作为你的一个域产生了，私有的 `private` ，妥妥的。谁也别想动。

      你认识很多朋友，你可以和每个朋友做一番大事业，解决一些问题，

      于是你的能力产生了，公共的 `public` 。

      你挣钱了，你的儿子可以继承你的，你也可以继承你父母的，但是你不能继承你儿子的，

      你父母也不能继承你的，这就是继承关系，只存在上下。且是单向的，因为辈分不能乱嘛。

-----

#### 域通常是私有的 private

#### 方法是公共的 public

## 具体权限

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/access.png?raw=true" height="500" width="1250" />
</div>


- 简单总结

    - public —— 公有的        所有类可见

    - protected —— 受保护的   同包类、子类可见  protected 如果要访问 A 包的域，B 包要作为子类继承 A 包Super类，然后才可以访问.

    - default —— 默认的      同包可见，子类不可见

    - private —— 私有的      同类可见，子类不可见         声明为 Private 变量，只能通过所在类的 get 方法被外部类访问。主要用来隐藏实现细节和保护类的数据。

-----

## 静态的 static

Static `static 修饰变量属于 静态变量 也叫 类变量(类初始化时，第一时间加载)，级别比较高 等同于 域 、成员方法、构造方法`

- 静态变量、静态方法都是独立于对象的，创建时 JVM 编译器为整个类创建了静态变量的副本 copy，所以静态块的执行顺序是第一的。

- 静态方法只能访问静态变量 `因为静态方法不操作对象，只访问自身类的静态变量`

- 静态方法不能直接调用非静态方法

- 静态方法中，不存在当前对象，也就是不能有 this,super，`不操作对象`

- 局部变量不能使用 static `因为局部变量级别太低，静态变量是位于 class 级别下的`

- 构造方法不能使用 static `因为一旦 static 修饰构造方法，还怎么调用该类中的非静态方法呢？`

- 静态方法不能被非静态方法覆盖 `因为 JVM 编译器为整个类创建了静态变量的副本 copy，且只分配一个内存空间`

- static 修饰域时，调用构造方法时，不会调用。

----

## 最终的 final


- final域 显式初始化，且只初始化一次

- final域 被 final的对象不能指向不同的对象，但final对象的数据可以被改变.

- final方法 不能被重写。`保证安全性`,但是可以重载。

- final 类  不可以被继承，不能做为父类。

----

## 抽象的 abstract

- abstract 类，抽象类中可以有抽象方法，也可以没有。但有抽象方法的类，必须是抽象类。`判断是否为抽象类的根据`

- abstract 类，必须有子类。因为抽象方法没有实现方法，必须由子类实现。

- abstract 类，任何继承抽象类的子类，都必须实现父类的所有抽象方法，除非子类也是抽象类。对子类进行约束和限制。

- abstract 方法 不能被声明为final,static

- abstract 方法 必须由 ; 来结束，而不是常规的 方法体 — { }，`因为抽象方法不能有具体的实例对象,需要子类来实现`。

- private 不能修饰 abstract ,因为抽象类的抽象方法必须要被子类全部实现，而子类却不能继承 私有的 抽象方法。

- abstract 类，不是不可以实例化，而是不能直接被实例化。`因为要实现抽象方法，new 出来的对象不能实现抽象方法`。但可以用匿名类来实例化。

- 匿名类实例化抽象类

        // anonymous  /ə’nɒnɪməs/ 匿名
        public class AnonymousInner {
            public static void main(String[] args) {
                SuperClass superClass = new SuperClass() {
                    @Override
                    void method() {
                    System.out.print("抽象类实例化");
                    }
                }; // 注意这个冒号，没有会报错。;表示分割。
                superClass.method();
            }
        }

        abstract class SuperClass{
            abstract void  method();
        }

        输出结果：
        抽象类实例化



