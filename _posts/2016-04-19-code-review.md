---
layout: post
title: Code Review最佳实践
category: 技术
tags: CODE
description: 关于Code Review的重要性，我相信好的工程师都能认识到。
---

关于Code Review的重要性，我相信好的工程师都能认识到。 参考 "让Code Review称为一种习惯" 和 "从Code Review谈如何做技术"。

同时引用一下有人对Google Code Review的描述：

> The biggest thing that makes Google’s code so good is simple: code review. At Google, no code, for any product, for any project, gets checked in until it gets a positive review.

### Code Review 主要Revivew什么

#### Architecture/Design

##### 单一职责原则.

> 这是经常被违背的原则。一个类只能干一个事情, 一个方法最好也只干一件事情。  比较常见的违背是一个类既干UI的事情，又干逻辑的事情, 这个在低质量的代码里很常见。

##### 行为是否统一

> 比如缓存是否统一，错误处理是否统一， 错误提示是否统一， 弹出框是否统一 等等。

> 同一逻辑/同一行为 有没有走同一Code Path？低质量程序的另一个特征是，同一行为/同一逻辑，因为出现在不同的地方或者被不同的方式触发，没有走同一Code Path 或者各处有一份copy的实现， 导致非常难以维护。

##### 代码污染

> 代码有没有对其他模块强耦合 ？

##### 重复代码

> 主要看有没有把公用组件，可复用的代码，函数抽取出来。

##### Open/Closed 原则

> 就是好不好扩展。 Open for extension, closed for modification.

##### 面向接口编程 和 不是 面向实现编程

> 主要就是看有没有进行合适的抽象， 把一些行为抽象为接口。

##### 健壮性

> 对Corner case有没有考虑完整，逻辑是否健壮？有没有潜在的bug？

> 有没有内存泄漏？有没有循环依赖?（针对特定语言，比如Objective-C) ？有没有野指针？

> 有没有考虑线程安全性， 数据访问的一致性

##### 错误处理

> 有没有很好的Error Handling？比如网络出错，IO出错。

##### 改动是不是对代码的提升

> 新的改动是打补丁，让代码质量继续恶化，还是对代码质量做了修复？

##### 效率/性能

> 客户端程序 对频繁消息 和较大数据等耗时操作是否处理得当。
> 关键算法的时间复杂度多少？有没有可能有潜在的性能瓶颈。

其中有一部分问题，比如一些设计原则， 可预见的效率问题， 开发模式一致性的问题 应该尽早在Design Review阶段解决。如果Design阶段没有解决，那至少在Code Review阶段也要把它找出来。

#### Style

##### 可读性

> 衡量可读性的可以有很好实践的标准，就是Reviewer能否非常容易的理解这个代码。 如果不是，那意味着代码的可读性要进行改进。

##### 命名

> 命名对可读性非常重要，我倾向于函数名/方法名长一点都没关系，必须是能自我阐述的。

> 英语用词尽量准确一点（哪怕有时候需要借助Google Translate，是值得的）

##### 函数长度/类长度

> 函数太长的不好阅读。 类太长了，比如超过了1000行，那你要看一下是否违反的“单一职责” 原则。

##### 注释

> 恰到好处的注释。 但更多我看到比较差质量的工程的一个特点是缺少注释。

##### 参数个数

> 不要太多， 一般不要超过3个。

#### Review Your Own Code First

跟著名的橡皮鸭调试法（Rubber Duck Debugging）一样，每次提交前整体把自己的代码过一遍非常有帮助，尤其是看看有没有犯低级错误。

### 如何进行Code Review

##### 1、多问问题。多问 “这块儿是怎么工作的？” “如果有XXX case，你这个怎么处理？”

##### 2、每次提交的代码不要太多，最好不要超过1000行，否则review起来效率会非常低。

##### 3、当面讨论代替Comments。 大部分情况下小组内的同事是坐在一起的，face to face的 code review是非常有效的。

##### 4、区分重点，不要舍本逐末。 优先抓住 设计，可读性，健壮性等重点问题。

### Code Review的意识

##### 1、作为一个Developer , 不仅要Deliver working code, 还要Deliver maintainable code.

##### 2、必要时进行重构，随着项目的迭代，在计划新增功能的同时，开发要主动计划重构的工作项。

##### 3、开放的心态，虚心接受大家的Review Comments。



