# Lab 4 

> 本节目标：
>
> 1. 熟悉intellij的使用，并用intellij完成本次lab的编程任务
> 2. 熟悉for循环、switch语句  
> 3. 初探文件输入，加强字符串处理能力
> 4. 维护世界的爱与和平

## 使用intellij

> **IntelliJ IDEA**被认为是当前Java开发效率最快的IDE工具。它是一种商业化销售的[Java](https://zh.wikipedia.org/wiki/Java)[集成开发环境](https://zh.wikipedia.org/wiki/%E9%9B%86%E6%88%90%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)（Integrated Development Environment，IDE）工具[软件](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6)，由[捷克](https://zh.wikipedia.org/wiki/%E6%8D%B7%E5%85%8B)软件公司[JetBrains](https://zh.wikipedia.org/wiki/JetBrains%E5%85%AC%E5%8F%B8)在2001年1月时推出最初版。

在[lab0](https://github.com/java-a/lab0)中，我们曾简单提到过intellij。intellij在一些大型项目中的高效使得它备受各大公司的青睐，我们也将用它来开发我们的期中project[斗兽棋](https://github.com/java-a/project1)。

为了让大家尽快上手，机智善良的@lfs TA已经为大家录制了十分详细的[Intellij入门视频](http://www.bilibili.com/mobile/video/av6483923.html?from=groupmessage&isappinstalled=0)，相信大家已经逐步感受到了IDE的便利。这次lab我们就需要在Intellij进行编程，并运行我们自己程序。

开始编程之前，我们先新建一个专属这次lab的project吧✌️

1. 新建project

   可以在welcome界面单击`Create New Project`，如图![img](https://cloud.githubusercontent.com/assets/9759891/19218336/b7037080-8e29-11e6-9fb6-a3b01b150509.png)

   或者，在菜单栏中依次单击`File` -> `New` -> `Project...` ，如图

   ![img](https://cloud.githubusercontent.com/assets/9759891/19218380/e207e972-8e2a-11e6-9d25-c4d522b41192.png)

2. 在最左一列选择Java后，其它设置不用改

3. 单击右下角的`Next`，跳到下一步，这里可以什么都不选；

   如果勾选`Create project from template`，并选择`Java Hellow World`，则最终新建的项目中，在src文件夹中会自动生成一个输出"Hello World"的java文件

4. 接下来是项目名及路径的定义。在`Project name`中填写你想要的项目名称，如`Lab4`，下方的`Project location`中也会自动更改路径名（`Project location`也不一定用自动生成的路径，可以单击右方的`...`进行选择）

   ![img](https://cloud.githubusercontent.com/assets/9759891/19218447/c58be774-8e2c-11e6-9265-f2d8861fde0f.png)

5. 单击右下角的Finish，则完成了新项目的建立。

6. 在当前窗口中，布局大致如下图，左边一栏是整个项目的层次结构，方便你查看需要的文件，右边则是打开的文件的详情。`Main.java`在`src`目录下，是自动生成的。

   ![img](https://cloud.githubusercontent.com/assets/9759891/19218474/9a215fdc-8e2d-11e6-869d-b3b844dbd301.png)

7. 运行这个project，可以直接单击右上角![](https://cloud.githubusercontent.com/assets/9759891/19218518/958ea0b4-8e2e-11e6-93ac-c34b8ad44cf0.png)的中绿色的三角形符号，或者也可以从菜单栏中依次单击`Run` -> `Run...`

   在今后的学习中，你的项目会越来越复杂，会有很多个java文件互相配合，那么哪个文件是你整个项目的入口呢？或者说，你想要直接运行哪个java程序呢？之前在`atom`里，我们运行的是当前窗口打开的这个文件，在intellij中呢？

   事实上，在java项目中，intellij会自动找到所有定义了`public static void` 的` main`方法的`public class`，如Step 6中自动生成的`Main.java`中的`public class Main`。如果你的项目中恰好有多个这样的`public class`，很可能就会列出所有这些类，并让你选择运行哪一个。像Step 7中图这样，是默认运行`Main`这个类；同样的，如果你有多个符合条件可运行的类，单击图中向下的三角形，你可以选择你想运行的类。

   所以你在这个project中最直接调用的java文件不一定要叫`Main`（比如project自动生成的这个），只要你想调用的文件中有`public static void` 的` main`方法就好了。

## 字符画

#### 问题描述

通过文件输入一个有意义的数字字符串，你需要将这条字符串“翻译”成字符画～

| number | output    |
| ------ | --------- |
| 0      | '  '      |
| 1      | 'X'       |
| 2      | '.'       |
| 3      | '\n'（即换行） |

### STEP 1 从文件读入字符串

在本次lab的同级目录下有待翻译的字符串文件`data.txt` ，请把它放置在和`src`目录同级的路径下。之前的课上我们学过可以用`Scanner(System.in)`读取终端中传入的参数，而如果我们把`System.in`换成一个文件，则可以输入文件中的内容了。

我们可以用下面这段代码来读取文件`data.txt`中的内容

```java
 File file = new File("data.txt");
 Scanner input = new Scanner(file);
 String dataString = input.next();
```

在这段代码中，`File`和`Scanner`都是java中已经定义好的一些工具类，需要显性地引用一下，你当然可以直接在文件最开始手动地输入

```java
import java.io.File;
import java.util.Scanner;
```

但是在intellij中，当你输入`File`或者`Scanner`这些关键字的时候，编译器会自动跳出你可以选择引用的工具类名称，你只需要选中想要的选择，这些工具类就会自动出现在文件最开始了😉

这看上去已经成功读入了文件内容了对不对？但如果你直接运行这段代码，应该会得到一段程序报错：

> java: unreported exception java.io.FileNotFoundException; must be caught or declared to be thrown

从字面意思上看来，就是你没有处理可能会出现的`FileNotFoundException`，这是一种常见的无法找到文件的异常情况。而什么是异常，这个具体会在今后学习`异常`的章节中详细说明。而在这次lab中，你只需要知道，当你要从文件中读入内容时，有很大的可能你希望读取的文件不存在（这些可能呢，比如手残打错文件名了，比如你的文件放错地方了，或者真的不存在这个文件），而为了各种目的（比如这个名字的文件不存在其实没关系，还有别的默认内容可以读取；或者后面的代码其实更重要，我不希望这个文件错误搞崩之后的代码运行），我们需要对这种文件不存在的情况进行处理，并且最好留下log报告给开发者。

再次感谢智能的intellij🙏它给出了解决这种异常的可能的方案，我们这次lab用这种自动给出的处理方案就足够了。如图，当鼠标点击到可能出错的这句话上时，这句话开头会出现一个红色的灯泡💡，表明有改进方案。

![](https://cloud.githubusercontent.com/assets/9759891/19218819/54070b74-8e36-11e6-808c-2e2fceff2645.png)

而我们单击这个红色灯泡，选择`Surround with try/catch`，就有自动的解决方案。

```java
try {
   input = new Scanner(file);
} catch (FileNotFoundException e) {
   e.printStackTrace();
}
```

这样，这段读取文件内容的代码就不会报错了。新的代码的意思是，编译器先尝试（try）运行一下可能出错的代码段，如果捕捉（catch）到了`FileNotFound`这个异常，就输出导致这个异常的一系列代码调用路径。

### STEP 2 从字符串读取想要的信息

接下来我们需要对输入的信息进行处理，完全就是字符串处理的工作了。因为将密文字符串“翻译”成字符画，是字符与字符的对应，所以我们要获取单个字符。这时我们需要用到`charAt`函数，使用方法同上次lab中出现的`substring`类似，如下代码即可获得`dataString`第`i`位的字符了。

```java
char theChar = dataString.charAt(i);
```

### STEP 3 密文翻译

对照问题描述中的翻译表，我们可以得到一些一一对应关系，请用`switch`语句实现。比如

```java
switch (theChar) {
  case '0':
    System.out.print(' ');
    break;
  default:
    System.out.println();
}
```

## 思考题

### 1. 多行输入

我们这次lab需要读取的文件内容只有一行，所以用

```java
 String dataString = input.next();
```

完全足够。而大多数情况下，文件中绝不只有一行内容需要输入，请思考一下需要怎么改这段代码。

### 2. 地图输出

在期中project斗兽棋中，我们需要读入初始的游戏地图，也是类似的多行输入。而地图中出现的元素较多，有0-8总共9种情况。如果用if或者switch语句进行一一对应肯定可以实现。但这样代码量较多，而且这些对应关系不仅仅在地图的输出中会被用到，其它代码逻辑中也可能被用到。如果每次都用条件判断，会过于重复。那么应该如何对应呢？

*希望大家自学数组的部分内容，尝试用数组而不是条件判断语句完成lab3和lab4☘️

## 一些链接

1. [课程代码风格指导](https://github.com/java-a/lab3/issues/3)
2. [Intellij入门视频](http://www.bilibili.com/mobile/video/av6483923.html?from=groupmessage&isappinstalled=0)
3. [好玩的代码注释](https://www.zhihu.com/question/20727260)