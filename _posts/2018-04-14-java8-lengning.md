---
layout: post
title: 写给大忙人的JavaSE8读书笔记（一）Lambda表达式
date: 2018-04-05 21:05:39
category: "java"，"Lambda表达式"
---

##Lambda表达式

含义：什么是Lambda表达？
lambda表达式在Java中就是一段匿名函数的代码。函数式编程中这段代码叫做函数。跟java原有的匿名内部类很像，但是实现原理和代码简洁性匿名内部类好。这段代码在Java8中通过一个java.lang.function包中的Function接口进行定义（函数式接口）
比如：我们获取文件目录下子目录时，传入FileFilter通常用Lambda表达式写法为：
     
	File file=...
	file.listFiles(d -> d.isDirectory())
    //or
    file.listFiles(File::isDirectory)
没有lambda表达式时，写法为：

    file.listFiles(new FileFilter() {

			@Override
			public boolean accept(File pathname) {
				if (pathname.isDirectory()) {
					return true;
				}
				return false;
			}
		});

可以看到通过lambda表达式，提供更好的代码简洁性和可读性。

一个Lambda表达式通常包括3个部分：

- 参数（可能为空，没有参数）
- 一段代码（lambda表达式的主要代码段）
- 自由变量的值（不是参数，不是lambda表达式内部代码段定义的变量）

其中含义自由变量的Lambda表达式通常就是所谓的“闭包”。

使用场景：什么时候使用Lambda表达式？
所有的Lambda表达式都是延迟执行的。这里的“延迟执行”场景包括：

- 在另一个线程中运行代码
- 多次运行代码
- 在某个算法的时间点运行代码
- 某些事件发生时运行代码
- 在需要使用的时候运行代码

注意：延迟执行不是说代码是异步执行。

###函数式接口
只包含一个抽象方法的接口叫做函数式接口，可以认为Java中所有的Lambda表达式都是某种函数式接口的实例。函数式接口是Java lambda表达式的模型定义。函数式接口通常用：@FunctionalInterface注解。

注意：
java是强类型语言，如果将一个lambda代码块赋值个一个函数式接口变量，需要处理检查期异常。
比如，你可以将如下代码：
    
	Runnable fPrint = {()->System.out.print("XXXX");};
赋值给Runnable接口变量，fPrint，但是如果lambda表达式会抛出异常，该赋值就会报错。如：

    Runnable fPrint = {()->System.out.print("xxx");Thread.sleep(1000);};
需要用Callable<Void>接口进行声明：

	Callable<Void> fPrint = {()->System.out.print("xxx");Thread.sleep(1000);};

此外Java8中为了支持Lambda表达式，对接口定义做了修改，Java8之前，对于接口只会包含：

- static final 的常量（默认public）
- 抽象方法

Java8之后还可以添加：

- 默认方法
- 静态方法

示例如下：

	public interface IWorkEngine {

		public static final String DEFAULT_NAME = "scorch";

		public void work(WorkEngineContext context);

		public default String getName() {//默认方法
			return DEFAULT_NAME;
		}
		public static void checkNameIlegal() throws ScorchException {
			if (DEFAULT_NAME.startsWith("sc")) {
				throw new ScorchException("name valiad");
			}
		}	
    }

