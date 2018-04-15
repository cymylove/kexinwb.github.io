---
layout: post
title: 写给大忙人看的JavaSE8读书笔记（二）Stream
date: 2018-04-15 21:05:39
category: [Stream]
tags: [Stream,java]
---

#### Stream

什么是Stream？
Stream支持顺序和并行聚合操作的一系列元素，为了执行计算，流操作被组成一个流管道。
集合和流，虽然有一些表面上的相似之处，但却有不同的目标。集合主要关注对它们元素的有效管理和访问。相比之下，流不直接访问或操纵元素，与之相反，流主要提供对集合进行的各种操作。

- 流自己不会存储元素，元素存储在原始的集合中，或者根据需要产生
- Stream的操作符不会改变源对象
- Stream操作时延迟执行的，在最后需要结果的时候才会执行。

使用Stream通常保含3个流程：

1. 创建一个Stream
2. 在一个或多个步骤中，指定将初始Stream转换为另一个Stream的中间操作。
3. 使用一个终止操作来产生一个结果。该操作会强制它之前的延迟操作立即执行，在这之后该Stream就不会再被使用了。

比如如下代码，根据一个User列表，获取年龄超过20岁的用户，然后再将user列表终止收集结果为userId=>User的Map对象。

	List<User> userList = createUserList();
	Map<String, User> userIdMap = userList.stream().filter(u -> u.getAge() > 20)
				.collect(Collectors.toMap(User::getId, Function.identity()));

常见函数：

- filter操作：从一个T到boolean的函数，产生一个符合某种特定条件的新流。
- map操作：对流中的值进行某种形式的转换，生成一个新的流，如：获取一个User列表的所有name列表：

		userList.stream().map(u ->u.getName()).collect(Collectors.toList());

- limit操作： 提取流中的n个元素，如果流没有这么多个元素返回流本身。

		userList.stream().limit(20);

-  concat操作： 连接两个流。
-  skip 操作： 丢掉前面n个元素，从1开始。


聚合方法


