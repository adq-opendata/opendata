# Web工程协同开发

[TOC]

web项目开发是大多数同学进入码农生涯首先接触到的工作，网上已经有大把的资料可以查询，在这里仅做一个提纲挈领的描述，以方便大家对整个web项目开发有个宏观的了解，免得在开发过程中被某些个别问题/现象困扰。

## 什么是Web项目
首先说什么是web项目，在这里引用[wiki](https://en.wikipedia.org/wiki/Web_project)上的定义
> A web project is the process of developing and creating a web site, activities in a network which are aimed at a pre-defined goal. The network can be both accessible for everyone, as in the internet, or only for certain people, as an intranet. The goal of web projects is the transfer of static and dynamic content - both directly to end users, as well as indirectly through means of various kinds of interfaces. Web projects are based on TCP/IP (Transfer Control Protocol/Internet Protocol) technology and concern the transfer of static and dynamic content. A web project involves many aspects, including programming[1] and the accompanying software development, web business, web server and network administration, hosting, graphics/design, the development and administration of databases, construction of interfaces, project management and quality assurance, search engine optimization, the maintenance of data in content management/editing systems and much more. Programming for a web project may be accomplished using one or more markup languages[2] (such as HTML, XML), scripting languages (PHP, Perl, JavaScript for example) or even more complex programming languages (such as Java, C/C++/C#).
When hosting a web project, the primary objectives include the provision of the necessary hardware and software infrastructure, and an assurance that the highest possible levels of availability and reliability are be offered.[3] Graphic/web design for web projects must offer a high quality of use for persons interacting with the website.[4] Agile project management methods (e.g. Scrum)[5] are used for the management of modern web projects in order to respond to changes in customer requirements and constraints as the project progresses. The project manager is responsible for the efficient and result-oriented programming of the web project.
>
> ---
>
>一个web项目就是开发并创建一个web网站的过程，在网络上以一种预定义的方式存在。这个网络可以被互联网上的任何人访问或在局域网内给特定人访问。而web项目的目标就是传播静态和动态内容，可以直接传播到终端用户，也可以通过多种API的手段间接传播。web项目是基于TCP/IP技术来传播静态和动态内容。一个web项目涉及到多种技术，包括编程、与编程相应地软件开发、web商业、web服务和网络管理、主机、界面设计、数据库的开发和管理、接口定义、项目管理和质量保证、搜索引擎优化、在内容管理/编辑系统中的数据维护，等等。web项目的编程语言涉及到一或多种标记语言（如：HTML、XML）、脚本语言（PHP、Perl、JavaScript）、甚至更复杂的编程语言（如：Java、C/C++/C#）
当部署一个web项目，最主要涉及到必要硬件和软件基础设施的准备，确保提供更高的可用性和可信赖性。web界面设计要给用户提供更高质量的交互性。现代的web项目还会使用敏捷项目管理方法以快速响应用户需求变更并在项目进展过程中对项目进行约束。项目管理者要为web项目的效率和面向结果编程负责。

可见，一个web项目涉及到了非常多的技术方面。即使在某些技术上实现了选型，web项目也必然会横跨多种技术，比如我们选择HTML、JS、Java、Mysql数据库等，仍需要熟悉并了解这涉及到的多种技术，只有在对这些相关技术有了深入了解之后才能更好地使用这些技术实现相应的功能。
当然在实践活动中，我们对一个web项目是有预先选择技术的，比如在我们现在的项目中就重点是用了如下几种技术：
- HTML+CSS
- JS
- Java
- Mysql

其中HTML+CSS就决定了前端的样式布局相对位置等，而JS则为前端的丰富效果提供了更大的灵活性。而Java作为后端服务语言，能够提供强大的编程能力，和丰富的类库。使用Mysql则有着选择了一种方便的数据存储方式。
后续我们将以这些技术为基础进行展开，有关这些技术的学习内容和相关资料会在study目录下进行后续更新和添加，争取让每种技术都能有条理清晰，让每个接触到相关内容的人都有迹可循，并有清晰的road map。

## 从访问网页说起

当我们在浏览器（browser）输入一个url，按下回车，然后获得一个良好排版展示的页面。以上是我们每个人（今天这个时代几乎所有接触到电脑的人都会进行上面的操作）每天习以为常的动作，那在这个过程中都发生了些什么？这个过程真的是这么显而易见的么？接下来，将简要说说上面的过程都涉及到了什么内容。
1. url解析。url只是人类方便记忆的一种发明，比如www.baidu.com，url会在我们的hosts中查找其对应的ip，查找不到会到域名服务器（dns，domain name server）进行相关url的查找，获得查找结果（ip地址，internet protocol address）。所以url解析将获取到一个ip地址，当获取不到相关地址时会将`找不到 www.adsfjlaskdjfl.com 的服务器 DNS 地址。`类似的信息告诉给浏览器。
2. 利用ip地址访问对应的网络服务。当获取到ip地址，会与这个ip地址进行网络协议（tcp/ip是最通用的一种）的通讯。这又是一个详细而具体并十分基础的内容，详情可以在网络协议相关内容中查看，这里不展开论述。总之可以将基于网络协议的通讯想象成两个人再打电话，只是机器会更严谨/傻一些，这个过程必须按照固定协议/规则进行。
	1. 服务端会将客户端（浏览器）请求的静态内容发送过来，包括HTML、CSS、JS、图片等。
			相关技术可以再进一步展开，这里不详述
	2. 服务端会将客户端（浏览器）请求的动态内容发送过来，可以是XML/Json等样式。

后续大部分内容都是网络协议的具体内容，不再展开具体描述。
## Web项目构成
当具体到一个java的web项目后，事情/问题就逐渐清晰和明朗了。首先web项目是由浏览器+服务端协同工作的。服务端负责提供各种静态资源/动态数据，而浏览器端则会根据需要向服务器端进行各种形式/参数的请求。这样一来可以将web项目简单分成**后端运行部分**和**前端运行部分**。

### 后端运行部分
所谓后端运行部分，主要是指运行在服务端的给前端供动态数据的部分。这一部分主要是action响应及以下部分，主要包括：网络服务（server）、数据访问（dao）。其核心对外提供的就是HTTP的访问接口，可以通过POST/GET/PUT等请求方式，将参数带给server，而server经过运算后将结果响应给前端浏览器。

### 前端运行部分
所谓前端运行部分，其是其初始代码仍在服务器上，只是由于浏览器通过请求第一个页面（往往是index页面），逐步将需要的HTML代码、CSS代码、图片、JS等静态资源拉到浏览器端，这样一来前端可运行可渲染的所需要的代码就都来到了浏览器端。而浏览器通过CSS、HTML对需要展示的内容进行布局和渲染，将JS运行在浏览器上，实现多样的动态效果。同时JS还可以与server端进行通讯，使用HTTP协议就可以与后端实现联动效果。

## 典型web项目的代码目录

TODO **坚煜补充**

## 独立开发Web项目

当一个人负责整个的web项目的开发时，其需要对诸多的技术有涉猎，并能够将其有机组合实现具体的业务功能。这个时候作为开发人员往往会忽略业务之外的内容。比如协作的问题、版本的问题、依赖管理的问题、统一开发环境的问题等。
独自开发项目时更多的着眼点在功能上，在业务逻辑实现上。由于是一个人，就不会凸显协作的问题，所有事情的前因后果自己都是很清楚的，也就不会注意一些细节，毕竟每个细节都是自己完成的，随时都可以回忆起当时的情况，并进行进一步修改。

## 协同开发注意事项

在协同开发过程中，每个参与者都按照约定的规范进行操作，会使得团队的效率大大提升，这样的规范操作能够避免团队注意力分散，而是团队聚焦在真正有产出的事情上。后面主要从**协作、版本、依赖管理**几个角度重点说明相关内容

### 协作
协作能够给团队中的每个人统一基础环境，我们需要进行统一的内容主要有：
- JDK，要统一版本
- IDE，要统一版本
- tomcat，要统一版本
- 工具同一版本，包括：版本管理工具、依赖管理工具、插件等
- 浏览器，要统一版本
- 数据库，共用一个数据库url，避免每个人创建local的数据库
- maven，使用maven管理依赖关系，不使用ide自带的依赖管理

可能有人会觉得浏览器干嘛还要统一？不同浏览器不正好测测兼容性么？这就涉及到工作当前的重心在哪里，如果工作重心在业务逻辑开发，那么就不要干扰整个业务开发的过程，可以在业务逻辑完善基础上再进行详细地兼容性测试。

### 版本控制
这里就涉及到版本管理工具如svn、git，它核心提供了：归档、版本控制、分支、融合等协作开发过程中需要的功能。

### 依赖管理
依赖管理目前普遍使用的是maven，它提供了一种定位依赖jar包的方法，通过组ID、工件ID、版本号来唯一定位一个jar包。而整个项目的依赖内容都可以在pom中指明，这样就避免的ant时代jar包到处拷贝的情况。

## 开发过程中的小技巧


---
TODO 这个文档有待继续完善，后续时间充裕继续补充内容。