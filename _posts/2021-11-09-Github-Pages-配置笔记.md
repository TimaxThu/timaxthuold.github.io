---
layout:     post
title:      Github Pages 配置笔记
subtitle:   
date:       2021-11-09
author:     JmJin
header-img: 
catalog:  true
tags:
    - 配置

---



# 说明

记录一下我最近配置GitHub Pages的问题



# 主题的一些问题说明 :(

【说明】这里记录一些我是用Pages时出现的问题，且目前没有想到好的解决办法（或者并没有解决办法...）

* 文章的catalog无法显示出标题的**分级信息**：md的标题有1~6个不同等级，但在文章右侧的目录中仅能显示标题文字信息，显示不出来级别信息
* 不间隔空行并没有起到分段作用：
  这个比较难叙述：在md中如果两行文字中间不空格，在Typora和CSDN上会显示为另起一行且无间隔（有空格时另起一行有间隔）；但是page上直接显示为一行了，没有另起一行。
* ...



# 21-11-09-博客终于修好了

【问题描述】

昨天开始博客突然渲染各种文章都失败，Page Build给出的问题是`/_layouts/post.html` #￥@#%@...（我也看不懂，[类似这样](https://github.com/TimaxThu/timaxthu.github.io/runs/4137318459)的报错）。但这个文件已经三年没动过了，很明显不是他的问题。我一时有些摸不着头脑。

今天查看了一下Github上的`commits`，发现在前几天提交完改后的about.html后build的文章就都失败了。那天我还有印象。于是我看了一下版本控制，commit显示删除了Gittalk评论部分的代码，于是我赶紧加上，而后，这个问题就解决掉了。文章post成功！check

【疑惑】

当时删除gittalk是因为我的博客并没有打开评论功能，我以为删去那串代码没关系，但没有想到会产生这样的反应。
不太清楚为什么





# 21-11-09-Latex的处理

【参考链接】[让GitHub Page支持Latex公式](https://syz913.github.io/2020/05/28/latex/)

【问题描述】

Github Page中的Jekyll仅仅支持很基础的markdown功能。所以不支持以下语法：

* 扩展的HTML语法，例如`<font color = red>显示红色</font>`
* Latex公式，例如`$\alpha$`
* 用`==`进行文本高亮

> 在PC上我的markdown都是用 `Typora` 这个软件写的，以上的语法Typora都是支持的，这里又要表扬一下，真的很好用！

上述的这些功能中Latex是很重要的功能，其他markdown扩展语法我还没研究除解决办法。

【解决办法】步骤如下

1. 在配置文件`_config.yml`中markdown的引擎已经为kramdown了，实际上不用调整。
2. 在想要支持Latex语法的文章前面（文章最上面yaml的下面）附上如下代码：

```html
 <head>
     <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
     <script type="text/x-mathjax-config">
         MathJax.Hub.Config({
             tex2jax: {
             skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
             inlineMath: [['$','$']]
             }
         });
     </script>
 </head>
```

