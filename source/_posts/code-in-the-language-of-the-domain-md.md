---
title: 程序员应该知道的97件事-11 使用领域内的语言编码
date: 2020-11-23 17:25:30
tags:
	- 程序员应该知道的97件事
categories:
	- 英文文章翻译
---

原文链接: {% link Code in the Language of the Domain, https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_11/,  https://uploads-ssl.webflow.com/5c349f90a3cd4515d0564552/5c66e5b48238e30e170da3be_logo.svg %}

## {% span blue, 使用领域内的语言编码 %}
展示两端代码库。第一段如下:
{% codeblock lang:java %}
if (portfolioIdsByTraderId.get(trader.getId())
	.containsKey(portfolio.getId())) {...}
{% endcodeblock %}
你挠挠头，想只掉这段代码是做什么用的。看着好像是从一个trader对象里获取ID信息，显然是从一个map的map结构中获取一个map，然后看portfolio对象的ID是否存在于这个内部映射里。你更纳闷了，查询portfolioIdsByTraderId的定义，你会发现一下内容: 
{% codeblock lang:java %}
Map<int, Map<int>> portfolioIdsByTraderId;
{% endcodeblock %}
渐渐地，你可能意识到这可能跟一个trader拥有一个特定porfolio访问权有关。当然，你可能还会找到相同代码片段-或者相似但略有不同的代码-无论什么时候，只要一个trader想访问一个特定的portfolio。

另一段代码库如下:
{% codeblock lang:java %}
if (trader.canView(portfolio)) {...}
{% endcodeblock %}
这次你不用疑惑了。你不需要知道trader是如何知道的。也许这里隐藏了很多map中包含map的结构在里面。那都是trader的逻辑，不是你的。
<!-- more -->
你平时更喜欢使用哪种风格编码？

曾几何时，我们只有最基础的数据结构：比特、字节和字符(其实就是字节，但我们假装是字母和标点)。小数有些棘手因为十个数字在二进制中工作不好用，所以我们有几种大小的浮点类型。接下来是数组和字符串(特殊的数组)。然后我们有了栈、队列、哈希、链表、跳表以及很多让人兴奋的且真实世界不存在的数据结构。“计算机科学”就是花费大量精力完成将真实世界与限制性的数据结构映射起来。真正的大师还要知其所以然。

然后，我们有了用户自定义类型。好吧，这不是什么新闻，但它某种程度上改变了游戏。如果你的领域包含trader或者portfolio这样的概念，你可以用Trader和Portfolio这样的类型对他们进行建模。但是比这更重要的是，你还可以使用领域内术语对它们的关系建模。

如果你不是使用领域术语进行编码，而是创建了一套默认的(秘密的)协议，这里的int对应trader，而那里的int表示portfolio。(最好不要把他们搞混！)如果你想要使用算法片段表述一个业务概念（一些Trader不被允许查看一些Portfolio--这是非法), 在映射关系中找到一个存在的访问权限，这样做并没有给审计和合规人员带来任何帮助。

下一个程序员可能不知道这个秘密，所以为什么不让它更明确一些呢？使用一个键查询另一个键作为存在检查的方法并不是那么容易理解的。人们应该如何凭借直觉知道防止利益冲突的业务规则是在哪里实现的？

代码明晰领域概念可以让其他程序员轻松收集到代码的意图，比按照他们对领域业务的理解改造算法要容易的多。这也意味着当领域模型的演进-随着你对领域业务的理解深入-你也比较容易修改代码。再加上良好的封装，规则很有可能只存在一个地方，你可以修改它，相关依赖代码不会有察觉。

数月后接手的程序员会感谢你，而且这个人可能就是你。


