---
title: 【每日一翻】React和Vue.js2.0哪一个更好？
date: 2019-08-15 17:30:20
categories:
  - 每日一翻
tags:
  - Quora
  - React
  - Vue.js
---

![源自https://unsplash.com/](https://raw.githubusercontent.com/x13945/image-bucket/master/img/markus-spiske-70Rir5vB96U-unsplash.jpg)
_源自 unsplash.com_
[原文地址:**React vs. Vue.js 2.0, which one wins?**](https://www.quora.com/React-vs-Vue-js-2-0-which-one-wins/answers/152114765)

<!-- more -->

## 先说什么是 React.js 和 Vue.js

### React.js

`React`是一个用来开发用户界面的`JavaScript`开源库。它第一次被人所知是在**2011**年被**Facebook**用在自家的新闻流里，之后在**2012**年被**Instagram**使用。

直至今日，**Facebook**和**Instagram**还在开发和维护`React`，并且`React`不光能用来开发基于浏览器的网页应用，还能用来开发手机应用。这个框架的目标就是为了在多个平台上提供快速、简单和易操作的应用。

或许你已经在[这里](https://stfalcon.com/en/blog/post/javascript-frameworks-for-software-development)读过这篇关于哪些最常用的 JavaScript 框架的文章。无论如何，`React`还不能称得上是一个全面框架，它更像是一个功能库。当你想把它作为一个框架来用的时候，你就需要添加一些第三方库来配合才行。

`React`的**长处**是速度快、轻量级、跨平台以及庞大的社区。

`React`的**缺点**就是必须要集成其他的第三方库工作良好，而这就导致了开发工作的复杂化。还有**一个缺点**就是`React`不像`Angular`和`Vue.js`那样，使用标准的`HTML/CSS`来开发。

![*SMN with React Component Released*](https://raw.githubusercontent.com/x13945/image-bucket/master/img/main-qimg-67ed54d37ceef239fc37029ca5af512a.png)
_SMN with React Component Released_

### Vue.js

`Vue`是一套用来构建用户界面的渐进式框架。与`Angulqr`和`React`不同的是，`Vue`被设计为

可以自底向上逐层应用。

这意味着开发者可以从特定页面逐步引入这个框架，这将大大降低开发的难度。

`Vue.js`的作者是**尤雨溪**，并且这个框架在中国的公司里被广泛应用。这些公司包括但不限于阿里巴巴、百度、小米等。不久之前，代码托管服务系统`GitLab`也切换到了`Vue.js`。

`Vue`优先处理的是视图层（也就是常说的 MVC 中的 View），这简化了和其他第三方库以及现有项目的整合。

`Vue`整合了`Angular`和`React`的长处：速度、轻量级以及支持其他一些技术的可能性，如`TypeScript`和`JSX`。但是，`Vue`依然可以使用传统`HTML`和`CSS`的代码标准。这加速了网页应用的开发，使项目开发和维护变得更容易。

因此，对于某些开发者，了解前端开发的基础即可用`Vue`来开发或维护项目了。

当下，当一个框架没有大公司背书的时候，没有大的开发者社区会是它的一个弱点。但是，`Vue`的流行度每年都在提升。

## 到底选哪个

在项目启动之前我们应当进行详细的分析和评估，但是每个项目基于自身背景都是独一无二的。不过，总有**几个关键点**，可以帮助我们选择开发时使用的技术：

### 速度，项目开发和支持的便利度

项目开发的速度取决于当前正在使用的技术。如果已经应用了`TypeScript`和`JSX`，那么就需要相应的使用`Angular`和`React`。

因此基于以上两点：当你从头开始一个项目的时候，最好选择`Vue.js`。

### 趋势

`Vue`、`Angular`和`React`都很流行，在以后几年内依然会统治现代开发市场，因此选择任意一个框架都不会是个错误。但是`Vue`正在获取越来越多的欢迎度，并且已经超过了`React`。在下面的表格中，你可以看到**Github**上这几个框架的*star*数量的趋势

![Frameworks’ popularity on Github](https://raw.githubusercontent.com/x13945/image-bucket/master/img/main-qimg-98753c0f9c4df6071f0902b18c1c554b.png)
_Frameworks’ popularity on Github_

### 迁移及扩展性

假如你现在已经选择了一个框架，但是你想要切换到另一个。`Vue.js`将是最好的选择，因为重写`Angular`和`React`项目就意味着你要把`TypeScript`和`JSX`代码重写为传统的`JavaScript`和`HTML`。

一个重要的**参考点**就是框架的**更新频率**。`Angular`**每 6 个月**就会有一次重大更新；`React`少一些，大概**每年一次**;`Vue`则相对稳定，**几年**内才会有一次重大更新。
