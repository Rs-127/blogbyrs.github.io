---
title: 关于渗透测试的那些事儿
date: 2024-08-25 23:52:40
tags: #标签
		- 技术
		- Linux
		- 信息安全
		- 渗透测试
categories: #分类
		- 网络安全
# Stretches the lines so that each line has equal width(文字向两侧对齊，对最后一行无效)
text align justify: true
---

# 正文前的碎碎念

敲下这些字，主要还是想记录一下自己入坑**信息安全**这行业以来，学过、见过、听说过、~~偷偷摸摸~~使用过的一些技术和工具，也想记录一下从入门到~~专家~~(**菜鸡**)的过程；

正文开始前的先声明：
本文以及后续相同标签、分类的文章中，可能会使用其他作者的技术、实例引用，文章中所有引用的内容都将会在文末点明并链接引用原文地址，若对原作者带来不便，请及时[联系我](mailto:glongg@yeah.net),我将第一时间删除与之相关的内容！

好了，正文开始。

---
## 前言
- 渗透测试 (Penetration test)并没有一个标准的定义，一些安全组织达成共识的通用说法是：通过模拟**恶意黑客**的攻击方法，来评估计算机网络系统安全的一种方法。这个过程包括对系统的任何弱点、技术缺陷或漏洞的主动分析，这个分析是从一个攻击者可能存在的位置来进行的，并且从这个位置有条件主动利用安全漏洞。
- 上述是书上/官方对渗透测试的定义，换成人话说，就是吃饱了没事干，找人打我一顿，看看我抗不抗揍，又或者买了个防弹衣，虎了吧唧的穿上，找人开枪试试防弹效果；(*开玩笑*)
- 渗透测试就是给网络系统来一次实战性质的模拟演练，从而达到安全测绘的目的。通过渗透测试，可以把网络系统中可能存在的薄弱点挖掘出来，并清晰知晓系统中存在的安全隐患和问题；


> 一名优秀的渗透测试工程师等于一个非常厉害的白帽子，也就是黑客。

> 不过需要注意的是，在进行渗透测试之前，**一定一定一定**要**得到客户的授权**！拿到**授权凭证**才可以进行渗透工作；
>如果在未授权的情况下，擅自进行了渗透工作，后果请参考[《中华人民共和国刑法》](https://baike.baidu.com/item/中华人民共和国刑法/721359)和[《网络安全法》](https://baike.baidu.com/item/中华人民共和国网络安全法/16843044?fromtitle=网络安全法&fromid=12291792)。（~~你要是能做到不留一点痕迹，就当我没说~~）

# 我是如何入坑信息安全行业的

上学读书那会儿，觉得老师教的计算机怎么跟我在电视上看的不一样啊？我看电影里的计算机大佬都是坐在咖啡厅、抱着笔记本、~~吃着火锅唱着歌突然就~~分分钟就黑进了CIA、FBI、~~KFC~~、MI6……可如果换成自己带着笔记本，坐在咖啡厅噼里啪啦一顿敲键盘的话……敲出来个Hello World？
> 太社死了。。。想不出来那画面
## 兴趣是最高的天赋

- 在大部分领域，主动学习和被迫接受信息完全是两码事，无论是效率还是质量。
- 进入信息安全这行最大的原因——感兴趣
	- > 感觉电影里的黑客很酷，动动手指就可以让一个或者多个地方紧张起来，很有心里满足感。（用现在的话说应该就是给我带来了很高的情绪价值？）
- 第二个原因——可观的收入
	- 可以去各大招聘网站上查看**渗透测试**或者**信息安全工程师**的’岗位薪酬报告’，香到流口水。
	- > 哥们的第一份实习工作是任课老师，每个月3000多块钱，（**没有任何诋毁这个职业的意思，老师是无上光荣的！**）还要天天跟学生斗智斗勇，改个作业直接血压飙升……
	- > 毕业之后，去了大城市，岗位是运维工程师，每个月不到7000块钱（他妈的，完全就是背锅侠啊！）干了两个多月后，偶然和一个学弟聊天，得知了他刚好在我这个城市参加[CTF比赛](https://baike.baidu.com/item/CTF/9548546)，就过去找他聊了聊，结果就得知人一场比赛下来的奖金都是5位数起的，并且还有企业在现场招人的，开的薪资待遇听的我是直流口水。果断开始整合资源并系统的学习，为转行做准备！
- 第三个原因——这行不卷啊！
	- > 现在的就业环境，其他行业我还不太清楚，但是运维、开发、金融行业……卷到让人崩溃！（~~这帮瘪犊子，咋就那么下力气呢！~~）
	- > 不过网络安全这个大行业目前还是良好的，需求日益增长，竞争相对没有那么大，一方面是因为这方面的人才确实少，另一方面，应该很少有学校会在课堂上教你如何渗透吧……
## 正八经入门的过程
-    因为之前读书时候，就有接触过这方面，所以对网络安全有了一个独属于自己的概念，再加上做的运维工作，也会一些Linux操作系统，所以，相对于我而言，上手还是比较快的。
- 在这我要先推荐或者吹嘘一波kali Linux操作系统，网安人员最爱操作系统之一，操作系统本身就集成了大量的各种类的“黑客工具”用于网安人员进行渗透测试工作。
    - > 依稀记得当初装好kali并且成功进入kali系统，并看到kali操作系统logo时候的那种心情，一切都是新奇的，瞎捣鼓了几个工具后忍不住感叹——“卧槽，网安就是干这个的！”哪像现在，来了个工作，一看内容，忍不住吐槽——“卧槽，网安就干这个？”

### 说回正题，想要入门网安，还是有一点点的门槛的。

   - 首先你要有计算机基础，最起码要会操作Windows系统，会使用cmd、powershell命令；
   - 其次要懂一些基础的计算机网络方面的知识，比如TCP/IP协议、**HTTP协议**、OSI模型；
   - 还要了解一些数据库方面的知识，比如最基础的数据库结构、默认的端口、sql命令等等；
   - 接着，最好还要懂一些开发语言方面的知识，不需要你非常精通，只需要可以看懂代码片段，明白这块代码大概是实现什么功能就可以。
   - > 去年我有个朋友想转行网安，之前是做实业的，完全没有接触过计算机行业，我就给他推荐了一下学习路线，结果这小子一头扎进python，最后搞开发去了……
   - 如果之前完全都没有接触过网安，现学的话，可以着重了解**HTTP协议**，因为现在大部分的渗透测试场景都是通过**web端**进行的，也称为**web渗透**。
   
   -  >很少会有客户允许你进行内网渗透的（~~虽然每个网安人都想打穿某个内网拿到system权限~~)
   -  整体来说，网安从业人员，抛开网安方面的知识外，对很多方面的知识都是略懂一二，称得上是**样样通，样样松**。

### 学习网安方面知识
- 上述所说的门槛知识都了解之后，可以开始接触正八经的网络安全方面知识；
- 网络安全是一个大的分类，存在很多分支，例如渗透测试、web安全、安全运维、安全服务、代码审计、操作系统安全等等。
- 上述的分支岗位，无论最后你想深耕哪个方向，都绕不开一个最关键的知识学科——linux操作系统。
    - > 对于网安从业者而言Linux操作系统基本上是必备技能之一了，因为许多工具、软件只能运行在Linux环境中
    - > 不过也不必觉得操作系统难学，相对于Windows，Linux不过是将Windows中的各种输入动作转换成了命令，操作模式还是给操作系统输入指令——操纵系统执行——操作系统输出信息；这是所有操作系统亘古不变的逻辑。
    - > 或许你会觉得，我在Windows中那么多操作都是用鼠标进行的，现在突然使用命令，记不住那么多命令怎么办呢？
    - > 完全不用担心，Linux命令大概300-400条，可是常用的命令也就20-30条，其余的都是软件或者工具的命令，这些工具的使用方法都可以使用[command] --help来查看
    -  > 或许还会有很多人觉得20-30条命令很多，其实可以回忆一下在操作Windows系统的过程中，无论你做什么操作始终绕不开**增、删、改、查**这四个动作。Linux或者说我们日常使用的所有软件、操作系统都一样，本质上就是在进行**增、删、改、查**这四个动作，所以只需要熟悉使用touch、rm、vim、cat/ls、就可以入门Linux了！
    -  > Linux精通确实很难，但如果只是熟悉使用，真的很简单！并且比Windows还要一目了然。

# 一些网络安全岗位必要的知识

---
好困，不想写。。。。
