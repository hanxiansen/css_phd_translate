# 《Cascading Style Sheets》博士论文翻译

- 原文 <https://www.wiumlie.no/2006/phd/>
* [译者序](#译者序)
* [摘要](#摘要)
* [灵感](#灵感)
* [致谢](#致谢)

* [一、介绍](#介绍)
  * [1.1结构vs展示](#结构vs展示)
    * [1.1.1抽象级别](#抽象级别)
    * [1.1.2表示性的HTML](#表示性的HTML)
  * [1.2样式表](#样式表)
    * [1.2.1 所见即所得——矛盾的模式](#所见即所得——矛盾的模式)
    * [1.2.2 web的特征](#web的特征)
    * [1.2.3 web样式表的机制](#web样式表的机制)
  * [1.3CSS](#CSS)


# 译者序

# 一、介绍

大约在1990年，Tim Berners-Lee设计了构筑万维网(world wide web)基础的三大技术规范：为web提供文档格式化的超文本标记语言(HTML)；为文档之间添加链接的Universal Resource Locators(URL)技术；为各机器在internet上传送文件的超文本传输协议（HTTP），这些技术的规范及实现都由CERN组织免费提供。

web世界快速发展，1993年，国家超级计算应用中心NCSA(National Center for Supercomputing Applications)推出了Mosaic浏览器，用户突然拥有了一个魅力浏览器，利用它可以在各个相互关联的文档之间进行网络冲浪了，伴随着用户量的激增，更多的创作者被web所吸引，更多的内容随之被传播。

在最开始，HTML只是一个简单的结构化文档格式，用来在文本字符串之间添加标签(tags)来指明文本的角色。例如：一个文本的字符串可以被标记为段落，同时另一些字符串可以被标记为可点击链接，这些元素在早期的HTML中，其逻辑性更胜其于呈现性。例如，HTML将会把一些文本标记为标题元素(heading)，但不会描述标题(heading)元素该如何呈现。文本的呈现-包括使用字体、颜色、大小等主要由浏览器决定。

## 1.1 结构vs展示

像CERN这样的科研组织更注重逻辑、结构和内容，而不是美学、意象和样式，这种结构化的观念反映到HTML设计中就表现为段落就标记为"段落"(paragraph)，标题(heading)就赋予一个级别编号，以指明它们在文档结构中的地位(译者注: 如h1、h2这种标题编号)。

由于web吸引了更多的科研组织以外的人，web创作者们开始抱怨他们没有足够的覆盖原生页面外观的影响力，新的web创作者们最常抱怨的一个问题就是如何更改元素的字体和颜色。以下内容是1994年初发送到www-talk邮件列表的邮件摘要，由此可以看出web创作者们和浏览器标准制定者的紧张关系(我在本章中引用了发送给开发者社区的邮件消息列表，并将在后续章节中反复引用，邮件列表对于早期的网络社区聚集至关重要，邮件列表的超文本档案在20世纪90年代初快速崛起并发展壮大，10年后的今天，这些档案为web的设计和开发提供了宝贵的视角)：
>In fact, it has been a constant source of delight for me over the past year to get to continually tell hordes (literally) of people who want to – strap yourselves in, here it comes – control what their documents look like in ways that would be trivial in TeX, Microsoft Word, and every other common text processing environment: 'Sorry, you're screwed.'

>事实上，在过去一年里，我不断的告诉那些成群结队(字面意思)的人——那些想要把自己绑在这里，试着像在Tex、Microsoft Word等常见文本处理软件那样在web上处理好文本展示的人：“哈哈，对不起，你完蛋了！”，这对我来说是一件无比搞笑的事。

这篇消息的作者是Marc Andreessen，他是流行浏览器——NCSA Mosaic背后的一名开发者，后来他成为了网景浏览器(Netscape)的联合创始人，网景浏览器通过在HTML中引入表示性的标签来满足创作者们的需求。1994年10月13日，网景公司发布了他们的第一款beta版浏览器，网景浏览器支持一组新的表示性HTML标签(如居中标签：center)，不久，更多的同类标签加入进来。

### 1.1.1 抽象级别
通过向html中添加表示性标签，它从一种抽象的、结构化的超文本标记语言(创作者们为文本标记不同的逻辑性角色(段落、标题、列表等))，演变为强调文档的最终呈现方式(字体、颜色和布局)的具体的表示性语言。
在传统的印刷出版时代，读者会收到经过处理后的成品印刷物，印刷物上的每个文字都有其固定的位置、形状、大小和颜色，读者无法更改其展现方式。然而，电子文档是半成品，必须经过装配(assembly)处理后才能呈现给人类读者，装配过程中(常被称为格式化(formatting)过程)，对如何呈现文档提供了多种多样的选择性。例如：浏览器在彩色屏幕上呈现文档时必须要选择要使用的字体和颜色。电子文档所需处理的等级将会因文档的不同格式而有很大的差异，电子文档类似于家具：有些家具已事先预装好，而有些家具买来时只是一个个打包的平面板子，需要买主自己组装好。如果一方文档需要做大量的处理，我们称其为较高级别的抽象，如果一份文档只需要少量的处理，我们则称其为较低级别的抽象。
确定合适的抽象级别是文档格式设计的重要环节，如果抽象的级别较高，创作和格式化的复杂度也会随之增加，创作者必须涉及到不可见的抽象概念，在接收端，如果元素的抽象级别较高，浏览器必须把高度抽象的元素转变为具体的对象，这将变得非常复杂，不过高级抽象也并非没有好处，它的好处是便于在多处上下文中复用，例如：标题元素可以在印刷文档中以大写字母的形式呈现，并且标题元素在文本朗读系统中将会具有更大的声音。
相反，较低的抽象级别将会使创作和格式化过程变得更加简易(在某种成都上来说),创作者将会使用所见即所得的富文本编辑工具(WYSIWYG)，并且浏览器在呈现视图的过程中也无需执行复杂的转换任务，使用“面向表现对象”的文档格式的缺点是——内容在其它上下文中难以复用，例如：难以在不同屏幕尺寸的设备上实现“面向表示对象”的内容，也很难让视力障碍者获取“面向表示对象”的内容。
将文档从一种格式转换为另一种格式时，两种格式可能处于不同的抽象级别，通常，可以将文档从较高级别的抽象转换为较低级别的抽象，但反之则不行。本论文将介绍一种度量抽象级别的“抽象阶梯”。

### 1.1.2 表示性的HTML
在HTML中引入表示性标签是“抽象阶梯”的向下移动，其中一些新元素(如闪烁标签(BLINK)等)仅对特定的输出设备有意义(毕竟，文本朗读系统中无法表示闪烁性文本)。HTML的创建者希望HTML的标签可以在多种设置中生效，但表示性标签威胁到了设备的独立性、可访问性和内容的复用性。
将HTML开发为面向表示的语言也改变了创作者和用户之间的权力平衡，结构化的文档在呈现之前必须经过浏览器的格式化处理，而用户可以在某种程度上影响到格式化处理过程，然而，如果用户取得的文档是最终形态的(已完成了格式化)，用户就无法影响到文档了。
web创作者们要求自己能对文档产生更大的影响力，并一直对这种改变翘首以盼，但在社区中也存在着很多持反对意见的人，许多人认为，在读者(而不是出版商)掌控的情况下，网络可以实现更具个性化的潜力，内容应该根据读者的偏好进行选择，多媒体和呈现的形式也应该是读者的选择。通过将html转换为表示性语言，有可能失去实现以用户为中心的“出版”模式的自由度。

## 1.2 样式表
在HTML由结构化语言演变为表示性语言的过程中，样式表作为一种替代方案被提出。术语“样式表”是传统出版体系中用来确保文档一致性的一种方法[芝加哥 1993]，在传统出版过程中，会在手稿上附带一份样式表，作为特定手稿措辞及语言规则的连续记录[Brüggemann-Klein&Wood 1992]。

20世纪80年代，随着个人电脑的普及，出版业发生了巨大的变化，电子出版提供了一些工具，可以简化从创作、编辑到打印的全部出版流程。在电子出版中，术语“样式表”是指一组关于如何呈现样式的规则，而不是如何创作内容的规则，样式表将由设计师指定，并在打印前发送给排字机，通常，它用来描述以文本为中心的文档布局及视觉展示(包括字体，颜色，空白)。

在本文，术语“样式表”指代一组规则，这些规则将文档元素中的样式属性和值与结构元素相关联，从而决定如何展示稳定。样式表通常不包含内容，可以在文档中相互关联，并且可以在文档中复用，这种定义就允许了“样式表”可以在电子出版和web世界中使用。

大约从1980年开始，样式表开始在电子出版系统中被使用(参加第2章和第3章)，与结构文档相结合后，样式表提供了内容和表示的延迟绑定(late binding)[Reid 1989]，意即：内容和表示在创作完成后才合并，这个理念吸引出版商的原因有以下两点：首先，可以在一系列的出版物中实现一致风格，其次，创作者再也不用担心内容的展现方式了，他们可以专注于内容本身。

事实上，一些作者发现在创作过程中不必担心细节表示是一种解放[Cailliau 1997]，然而，大多数作者最终使用了强调表示而不是结构的创作系统。

### 1.2.1 所见即所得——矛盾的模式
所见即所得 —— 是一种文档创作的矛盾模式，所见即所得程序不断更新最终的呈现方式，当创作者输入时，屏幕将会更新以反映该点打印文档时将呈现的页面布局。

和结构文档与样式表所采用的样式与内容的延迟绑定相比，所见即所得模式提供了即时绑定。所有的编辑操作都会即时更改最终的呈现。这种方案通常会导致作者过分强调文档的最终呈现(通常是打印文档)，而不是逻辑标签。

一些应用程序尝试将结构化文档和所见即所得的编辑模式相结合，包括Adobe的FrameMaker[FrameMaker]、Microsoft的Word[MS-Word]和W3C的Amaya[Amaya]，通常这些应用程序会为创作者提供文档的几个视图view，其中之一是所见即所得视图，其它视图为更具结构化的视图，这将使创作者通过所见即所得工具创作结构性文档，然而，使用所见即所得工具也存在风险：它们允许创作者进行纯粹的展示性文档修改时，会影响到文档结构的稳定性。

### 1.2.2 web的特征
研究表明，当以文本印刷为最终目的进行创作时，很难激发创作者在逻辑层面而不是视觉层面的创作热情，然而，随着web的出现，内容的可复用性得到增强，web文档不再局限于纸张上打印和分发了，而是通过电子形式传递到用户电脑上，文档分发转变为电子文档形式影响到了创作过程和样式表语言，其具有如下几个关键特征：

- 延迟绑定变为延后绑定：在web上，文档以电子的形式传递到用户加算计上，电子出版中内容与呈现形式间的延迟绑定在web上变得更晚了，这种绑定不再发生于出版社，而是发生在用户的计算机上，这种转变增加了呈现的自由度，但随之也带来了新的性能挑战，因为在“延后绑定”进行时，用户只得默默等待，此外，因为创作者不在最终呈现的现场，他没法保证最终的呈现是正确的。

- 以纸张为中心的出版模式转变到以屏幕为中心：在web出现之前，大多数电子文档最终都处理成打印文档，它们在计算机屏幕上完成编辑和处理流程，但它们大多在最后被处理成打印媒体格式，毕竟，在web上，大多数用户在屏幕上浏览文档。

- 单一传输转变为多元输出：尽管屏幕是web世界中的主要媒介，但也存在着很多其它类型，创作者无法知道用户到底使用哪种类型的输出设备，不再只有一个终极呈现形式，而是有很多个，因此，样式表必须能在各种输出设备上都能描述呈现方式。

- 创作者控制转变为传作者和用户的共同控制：由于内容和展现间的绑定发生于用户的计算机上，来自多个源头的影响可能组合形成为一种展现形式，考虑到这种自由性，用户以及创作者一个都有影响文档展示的能力，基于用户需求和偏好的个性展现成功可能，这将与其它发布模式产生区别，在其它发布环节中，创作者和出版社完成垄断了文档的展示。

- 独立稳定转变为超链接：web是个大量超链接文档的集合，以前表示为引用信息的文本现在表示成一个个超链接。

- 确定的传输转变成不确定：web资源广泛的分布在各种连接在一起的计算机上，资源不能用的可能性很高。另一个变化是，web比出版社的出版系统更可能失败，虽然使样式表可用时自然而然的，但可能资源并不总是会在客户端上可用。

因此，随着web的引入，样式表的重心由创作过程中的创作者工具转移到内容生成后的内容复用工具，web上的样式表可能比以纸张为中心的样式表更为重要，因为内容的复用可能性更大，正如样式表的性质由纸质出版转变为电子出版一样，web的样式表性质也发生了改变。

### 1.2.3 web样式表的机制

在CERN的NeXT设备上，第一个粗糙的样式表被硬编码到了在其上实现的第一个WWW客户端，但是，没有规定样式表的编写的规范，也没有指明样式表的语法规则，每个浏览器各自把页面以他们认为最好的呈现方式展示给用户。

在web上使用样式表的潜在好处是显而易见的，和不断改进的HTML相比，一个开发良好的样式表应给予创作者期望的更丰富的风格词汇，此外HTML还会 继续保留结构化的语法，以便它能运行在各种设备上。

因为这些原因，www-talk邮件列表(早期进行电子交流的网络社区)上的许多人都一致认为电子表将给web带来好处，但是，社区对于web是否需要一种新的样式表语言，或者采用现存语言中的一种(专为纸质出版而设计的)更合适，还存在着分歧。

1993年，几种专为web设计的样式表语言被提出(参见第四章: 网络样式表提案)，但它们最终都没获得成功，主要原因是因为它们没能获得浏览器的支持，只要Mosaic浏览器(迄今最流行的浏览器)不支持哪种样式表，创作者就没有使用它们进行编写的动力，此外，这些提案都没能发展成稳定版，一份成功的web样式表必须做到既能激发浏览器开发者的开发热情，又能激发创造者的创作热情。

## 1.3 CSS
在网景(Netscape)公司宣布他们最新浏览器的3天前，css开发者发布了web世界上的第一版css提案(Cascading HTML style sheets的缩写名)[lie 1994]，除了描述字体、颜色和文档布局之外(有几个提案已经完成)，CSS还引入了几个全新功能来强调web发布的改变，CSS的设计理念旨在允许创作者和用户都能对文档展示做出影响：
> The proposed scheme supplies the brower with an ordered list (cascade) of style sheets. The user supplies the initial sheet which may request total control of the presentation, but – more likely – hands most of the influence over to the style sheets referenced in the incoming document.
>
> 该提案为有序列表(级联)提供了样式，用户提供初始样式表(该样式表可能会完全控制文档的展示)，但更可能的是，大部分的文档展示还是交友文档中自身引用的样式表。

达成创作者和用户之间的成功谈判是CSS的主要愿景之一，如果成功，创作者将获得他们在文档展示上应有的影响力，不会觉得的他们是被迫来展示HTML和其它技巧，另一方面，用户可以自由的文档展示，他们既可以选择创作者制定的样式展示，也可以选择自己的样式展示。

其实在大多数情况下，创作者不会和用户产生冲突，当二者都不想给文档指定特定样式时，浏览器就必须带一个默认的样式表来对HTML进行默认展示，因此，关于CSS的定义将会有三个来源：创作者、用户、浏览器，CSS能够将这三者合并后来进行最终的文档渲染，我们将处理这几种样式的组合 — 解决三者之间可能出现的冲突的过程称之为“串联|级联(cascading)”。

### 1.3.1 CSS的发展
第一版css提案是本着公开交流web如何发展的精神而提出的，并且在公开的邮件列表中进行了讨论，许多人[Bos 1994][Behlendorf 1994][Wei 1994]对该草案做出了回应，促进了草案的进一步发展，在1995年期间，共发布了大约8次修订，该年12月份发布的最后一次修订版被选为稳定版，并鼓励浏览器厂商将该版本作为基础实现标准。

除了一些小的意外错误，19995年12月份发布的草案在语法上基本上稳定保持了下来，其中第一份部分关于css语法的介绍依然保持下来：

> Designing simple style sheets is easy. One only needs to know a little HTML and some basic desktop publishing terminology. E.g., to set the text color of 'H1' elements to blue, one can say:
`` H1 { color: blue }``
> The example consists of two main parts: selector ('H1') and declaration ('color: blue'). The declaration has two parts, property ('color') and value ('blue').

> 设计简单的样式表很容易，你只需知道一点HTML知识和一些基础的桌面出版术语，例如，要将'H1'标签的文本颜色设置为蓝色，可以这样说：
`` H1 { color: blue } ``
> 该例子包含了两个主要部分：选择器(h1)和声明(color: blue)，声明分为两部分：属性(color)和属性值(blue)。

1996年12月，CSS1规范成为W3C的推荐标准[CSS1 1996]。1998年5月，CSS2成为W3C推荐标准[CSS2 1998]，第6章(层叠样式表)将会更详细的叙述其发展史。

在第一版CSS天发布十年后，所有的主流web浏览器都支持了CSS，并且大多数网页都使用CSS，全面评估CSS本身及其对web的影响可能还为时尚早，但我们可以学习和研究css的设计，将其与其它样式表语言和香港方案做比较。

## 1.4 摘要和总结
在文的本章节中介绍了一些关键概念，HTML是为web开发的一种简单的结构文档格式，当web创作者要求他们能对文档产生更多的表示性影响时，HTML开始发展成为一种表示性语言，而不是一种结构化语言，为了让抽象阶梯停止向下滑动，CSS被开发为web的样式表语言，自1980年以来，样式表一直是电子出版系统中的一部分，在web上，样式表的焦点从创作过程中的工具转移到内容生成后的内容复用工具。

本文将详细地探讨为什么web需要不同于其它发布类型的样式表语言，以及这门语言是如何被设计出来的，然而，在探讨之前，还有必要探讨另外两个议题：首先，必须要理解结构化文档，因为样式表是应用在结构化文档之上的，其次，必须研究在web出现之前，样式表语言的发展情况，以此来确定这些样式表语言是否适用于web，这两项议题将分别在第2章和第3章中讨论。