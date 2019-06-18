# Spider Money作用  
本文档解释了如何将Mozilla JavaScript引擎SpiderMonkey嵌入到您的c++程序中。  
JavaScript广泛用于在浏览器中运行的客户端脚本。但是Mozilla的JavaScript引擎是一个库，可以链接到任何c++程序，而不仅仅是一个浏览器。许多应用程序都可以从脚本中获益。这些程序可以使用SpiderMonkey API从c++执行JavaScript代码。  
**注意:** FOSS wiki页面包含了一些指向其他库和程序的链接，这些库和程序可以使使用Spidermonkey和JSAPI变得更简单。（译文没有）  
## 1.1 什么是Spider Money？  
JavaScript引擎编译并执行包含JavaScript语句和函数的脚本。引擎为执行脚本所需的对象处理内存分配，并清理垃圾收集—不再需要的对象。  
JavaScript这个词可能会让人想起事件处理程序(如onclick)、DOM对象和打开窗口和XML Http Request。但是在Mozilla中，所有这些特性实际上都是由其他组件提供的，而不是SpiderMonkey引擎本身。SpiderMonkey提供了一些核心JavaScript数据类型(数字、字符串、数组、对象等)和一些方法，比如Array.push。它还使每个应用程序可以很容易地将自己的一些对象和函数公开给JavaScript代码。浏览器公开DOM对象。您的应用程序将公开与您想要编写的脚本类型相关的对象。由应用程序开发人员决定向脚本公开哪些对象和方法。  
## 1.2 Hello world  
### 1.2.1 使用SpiderMonkey库  
要从源代码构建SpiderMonkey，请参阅[SpiderMonkey构建文档](./002\ SpiderMonkey构建文档.md)。  

