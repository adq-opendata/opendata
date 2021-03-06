# Web工程分模块
[TOC]
一般来说，web项目最终会打包成war包，交给tomcat类的web服务容器来提供服务。那一个相对复杂的web工程会依赖很多第三方提供功能的jar包，并且会按照MVC的逻辑进行后端服务分层，通常会分成**web（controller）、service、dao**，当然为了方便逻辑的实现和管理还会添加诸如**util**包。这些内容就为后续的包管理埋下了隐患。

## 通常遇到的问题
1. 有外部程序使用了web项目中的util方法
2. web项目不同package由不同人负责，当某个人不小心提交了无法编译的代码，将影响整个项目的调试
3. 随着项目越来越大，每次build都要花费很长时间。
4. 我只想发布自己完成部分的代码，无法单独发布
5. 我希望有些web组件能够实现可插拔，比如：论坛、聊天室、邮箱系统等

## module及其简介
首先说下，在工程中的module实际上是代码的一个集合，其提出的初衷是实现模块化程序设计，实现模块内的**高聚合**、模块间的**低耦合**。

## 解决问题
使用module的思想可以有效解决web工程遇到的一些问题。比如可以将web项目的多种功能package分成不同的module，这样可以把util做成基础的module，后续如dao对应的module就可以依赖这个util的模块。看看上述几个问题是不是可以有效解决？

1. 外部使用util方法。由于util已经单独成为module，那么util的打包都是独立完成的，可以打成独立的jar包，所以外部程序使用util方法只需要把util打成的jar包被依赖，而跟整个web项目没有太多关系。
2. package由不同人负责，由于依赖是module依赖，外部调试可以调整各package的版本号，这样就使得其他部分进行调试时可以通过调整版本号就不会受到影响。
3. 项目变大，只是在build war包时会花费时间较长，只build部分模块时间不会太长
4. 某个package的代码完成了，可以单独发布成jar包，实现单独发布。
5. web组件可插拔，这个实现就不仅仅是层次上的划分，更是功能上的划分。可以考虑在划分module时同时使用层次和功能，如下表：

    |     |聊天室|论坛|邮箱系统|
    | --- |---|---|---|
    |web|模块11|模块12|模块13|
    |service|模块21|模块22|模块23|
    |dao|模块31|模块32|模块33|
    
	这样就可以对代码进行多模块管理，当需要打包时，只需要依赖特定的module即可。但要明确这里的限制：**功能模块必须是可切割的，相互之间不能引用，否则模块在功能之间就存在严重依赖，打包时会出现麻烦。**

## 其他
以上主要说明的是web工程中后台服务代码的打包，前端界面内容的切割并没有涉及到。但打包成war包时，是连带配置文件、前端代码、样式等一同打包的，那么对前端代码的模块化就是一个很大的问题。
这一部分*未完待续TODO*



