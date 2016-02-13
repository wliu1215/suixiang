<!DOCTYPE.md>
.md xmlns="http://www.w3.org/1999/...md" xml:lang="zh-CN">
<head>
<meta http-equiv="Content-Type" content="text.md; charset=utf-8" />
<meta name="generator" content="Python script by program.think@gmail.com" />
<meta name="provider" content="program-think.blogspot.com" />
<link type="text/css" rel="stylesheet" href="../../css/program-think.css" />
<title>如何开展灰盒测试[1]：灰盒测试优缺点分析 - 编程随想的博客</title>
</head>
<body>
<div id="main" style="width:100%;">
<h1><a href="../../index.md" title="回到首页">如何开展灰盒测试[1]：灰盒测试优缺点分析</a></h1>
<div class="post-info"><span class="date-header">2010-11-30</span><a href="../../tags/E7BC96E7A88B.md" class="tag">编程</a> <a href="../../tags/E7BC96E7A88B.E8BDAFE4BBB6E5B7A5E7A88B.md" class="tag">编程.软件工程</a> </div>
<hr>
<div class="post">
　　俺在忽悠某个技术领域的玩意儿之前，通常先要分析一下优缺点——这样才能调动大伙儿的积极性。所以，本系列第1帖先分析一下灰盒测试的优缺点。<!--program-think--><br /><br /><h2>★几个基本概念</h2><br />　　首先，把一些基本概念，简单通俗地说一下。如果觉得俺解释得不够好，不够细，可以自己去查维基百科的词条：洋文的在“<a href="http://en.wikipedia.org/wiki/Software_testing" target="_blank" rel="nofollow">这里</a>”，中文的词条在“<a href="http://zh.wikipedia.org/zh-cn/%E8%BD%AF%E4%BB%B6%E6%B5%8B%E8%AF%95" target="_blank" rel="nofollow">这里</a>”（可惜中文词条不够全，偏偏缺了“灰盒测试”这一节）。<br /><br /><h3>◇黑盒测试</h3><br />　　通俗来说：黑盒测试不关注软件内部的实现细节。他仅仅把被测试的软件当成一个整体来处理，只关注软件的外在表现，不关注内部细节。典型的黑盒测试，就是光拿着鼠标操作一下用户界面，看看功能是否满足要求。<br /><br /><h3>◇白盒测试</h3><br />　　白盒测试与黑盒测试相反，重点关注软件内部的实现细节（比如代码覆盖率等）。<br /><br /><h3>◇灰盒测试</h3><br />　　如果你是从事开发或者测试的行当，应该已经听过黑盒测试与白盒测试这2个概念。但对灰盒测试，或许比较耳生。单纯从名称上来看，灰盒测试是介于黑盒测试与白盒测试之间的一种测试方式。<br />　　这种测试方式，主要用于多模块构成的稍微复杂的软件系统。在灰盒测试中，重点关注软件系统内部模块的边界（接口）。这里所说的“接口”是广义的，包含有各种形式。对于进程内的模块，其接口可能是动态库的导出函数；对于进程级的模块，其接口可能是各种IPC（进程间通讯）机制；对于涉及数据库的软件系统，其接口可能是数据库的表结构......<br /><br /><h3>◇灰盒测试与黑盒测试的区别</h3><br />　　如果某软件包含多个模块，当你使用黑盒测试时，你只要关心整个软件系统的边界，无需关心软件系统内部各个模块之间如何协作。而如果使用灰盒测试，你就需要关心模块与模块之间的交互。这是灰盒测试与黑盒测试的区别。<br /><br /><h3>◇灰盒测试与白盒测试的区别</h3><br />　　但是，在灰盒测试中，你还是无需关心模块内部的实现细节。对于软件系统的<b>内部</b>模块，灰盒测试依然把它当成一个黑盒来看待。而白盒测试则不同，还需要再深入地了解<b>内部</b>模块的实现细节。所以，这是灰盒测试与黑盒测试的区别。<br /><br /><h3>◇灰盒测试与单元测试的区别</h3><br />　　刚才看到有网友在评论中问到此问题，俺补充一下。<br />　　首先，在进行单元测试时，需要写一些测试代码（行话叫“桩代码”，洋文叫stub）。一般来说，测试代码与被测试代码采用同种语言（比如Java的单元测试通常也用Java来写），且测试代码和被测试代码之间的耦合很紧密。因此，单元测试通常由开发人员来完成的——测试人员的能力未必能胜任。<br />　　其次，单元测试的颗粒度会更细（会细到模块内部的类一级、函数一级），而灰盒测试仅仅到模块一级。<br /><br /><h2>★相对于黑盒测试的优点</h2><br />　　灰盒测试相对黑盒测试的优点，其实有不少，俺挑几个重要的来说说。<br /><br /><h3>◇测试可以及早介入</h3><br />　　由于黑盒测试把整个软件系统当成一个整体来测试。如果系统的某个关键模块还没有完工，那测试人员就无法对整个系统进行测试，只好闲着没事干。而灰盒测试是针对模块的边界进行，模块开发完一个就测试一个。<br /><br /><h3>◇有助于测试人员理解系统结构</h3><br />　　为了进行灰盒测试，测试人员首先要熟悉内部模块之间的协作机制。在熟悉的过程中，“顺便”也就对整个系统（及其结构）有一个初步的、宏观的认识。这有助于测试人员发现一些系统结构方面的Bug。<br />　　而对于黑盒测试来说，由于测试人员不清楚软件系统的内部结构，难以发现一些结构性的缺陷。<br /><br /><h3>◇有助于管理层了解真实的开发进度</h3><br />　　一些复杂的大系统，经常会发生开发进度失控的情况。因为很多开发人员有报喜不报忧的倾向。当某个开发人员号称自己的工作已经完成了90%，往往意味着他/她还要花同样多的时间来完成剩下的10%。这导致负责项目管理的人，无法了解开发的真实进度。<br />　　由于灰盒测试针对对每一个模块进行，而且测试人员会从一个客观的角度来反馈模块的完成情况，这非常有利于管理层了解整个系统的真实完成情况。<br /><br /><h3>◇可以构造更好的测试用例</h3><br />　　如果仅仅用黑盒的方式测试系统的外部边界（通常是用户界面），有很多软件缺陷是不容易发现的。俺分别以B/S系统和C/S系统来举例。<br />　　假设开发一个复杂的（Windows环境下的）C/S软件。那么，这个软件通常不会仅仅只有一个EXE文件。它可能会有若干个EXE文件以及若干个DLL文件。假如某个DLL提供的导出函数，没有按照约定对输入参数进行有效性判断（比如指针是否为空），那你用黑盒测试的方式，难以暴露出这种缺陷。而灰盒测试就容易发现此类问题（具体如何发现，请看后续的“接口测试实战——测试进程内的模块接口”）。<br />　　假如你开发的是一个Web应用系统，那么，这种系统的服务端多半会提供若干个Web接口用于被客户端调用。假如某个Web接口存在安全性问题/并发性问题/健壮性问题/XX问题，你单纯用黑盒测试的手段，同样难以发现，而灰盒测试就可以搞定（灰盒测试是如何搞定的，请看后续的“<a href="../../2010/12/grey-box-testing-4.md" target="_blank">接口测试实战——测试跨主机的模块接口</a>”）。<br /><br /><h3>◇利于提升测试人员能力</h3><br />　　很多公司搞的黑盒测试，就是让测试人员用鼠标（键盘都难得用）操作用户界面。在这种的环境里，测试人员干的活，很多都是重复性的体力劳动，技术能力难以得到提高。<br />　　而如果搞灰盒测试，测试人员就需要多懂一点技术背景知识，必要时还得写点测试脚本，对测试人员的能力提升很有好处。<br /><br /><h2>★相对于白盒测试的好处</h2><br />　　灰盒测试相对白盒测试的好处，比较容易概括。简单来说，就是白盒测试较费钱（研发成本较高）。这多出来的研发成本，体现在如下几个方面。<br /><br /><h3>◇首先，招聘成本较高</h3><br />　　在人才市场上，100个应聘的测试人员中，未必能够找到一个合适的白盒测试人员。至少从俺及周围同事的面试经历来看，难得碰到具备白盒测试能力的人。所以，你可能要花很长时间才能找到合适的人，时间成本浪费掉了。<br /><br /><h3>◇其次，培训成本较高</h3><br />　　可能有同学会说，招不到就内部培养呗。这个说起来容易，但是培训也是有成本的。而且周期还不短，同样要耗费时间成本。<br /><br /><h3>◇再其次，人力成本较高</h3><br />　　物以稀为贵是一条普遍的经济学规律。由于能搞白盒测试的家伙是稀有动物，你自然不能给他/她开太低的薪水。否则人家待不了多久就跑路了。薪水开得高了，人力成本自然也就提高了。<br /><br /><h2>★其它的一些好处</h2><br />　　前面拿灰盒测试分别跟黑盒/白盒进行了对比，列举了一些优点。还有另外一些优点，和黑盒/白盒没啥关系，单独列在这里。<br /><br /><h3>◇顺便强化开发文档</h3><br />　　对于一个复杂的软件系统，模块之间的接口是很重要的，因此捏，接口文档也是很重要滴。而开发人员不爱写文档/不爱更新文档，（在软件业内）已经是臭名昭著了。很多软件开发到后期，模块之间的接口文档要么没有，要么和代码实现严重脱节。<br />　　但是，如果引入测试人员对模块之间的接口进行测试，就可以有效防止此种弊端。因为测试人员在测试前，首先要看模块间的接口文档，然后再根据接口文档设计测试用例，最后再执行用例。因此，一旦接口文档和代码实现不符，立马就露馅了。<br /><br /><h3>◇顺便搞搞自动化</h3><br />　　灰盒测试如果落实到位，还可以跟自动化测试相结合。从此可以大大提升测试的效率，进而大大提升软件的质量。（如何进行自动化的灰盒测试，后面的帖子会细谈）<br /><br /><h2>★灰盒测试有啥缺点？</h2><br />　　当然，凡事都有优点和缺点，灰盒测试自然也不例外。下面列举它的主要缺点。<br /><br /><h3>◇不适用于简单的系统</h3><br />　　所谓的简单系统，就是简单到总共只有一个模块。由于灰盒测试关注于系统内部模块之间的交互。如果某个系统简单到只有一个模块，那就没必要进行灰盒测试了。<br /><br /><h3>◇对测试人员的要求比黑盒测试高</h3><br />　　从上面的介绍来看，灰盒测试要求测试人员清楚系统内部由哪些模块构成，模块之间如何协作。因此，对测试的要求就提高了。因此，会带来一定的培训成本。不过捏，依照俺的经验，培训难度不大。稍微有点基础的测试人员，都可以在短期培训之后胜任。<br /><br /><h3>◇不如白盒测试深入</h3><br />　　显然，灰盒不如白盒那么深入。不过捏，考虑到灰盒测试相比白盒测试有显著的成本优势，该缺点不是太明显。<br /><br /><h2>★总结</h2><br />　　总而言之，言而总之，灰盒测试是一个很不错的东东，其优点明显而缺点容易克服。另外，俺前后在两家公司的研发部门推行过，效果不错的说。大伙儿值得去尝试一下。今天光说了优缺点对比，在<a href="../../2010/11/grey-box-testing-0.md">本系列</a>的<a href="../../2010/12/grey-box-testing-2.md">下一个帖子</a>，俺具体介绍一下，开展灰盒测试之前，管理上有哪些准备工作。<div class="blogger-post-footer">
</div>
<hr>
<div class="copyright">
<h4>版权声明</h4>
本博客所有的原创文章，作者皆保留版权。转载必须包含本声明，保持本文完整，并以超链接形式注明作者<a href="mailto:program.think@gmail.com">编程随想</a>和本文原始网址：<br>
<a href="2010/11/grey-box-testing-1.md">2010/11/grey-box-testing-1.md</a>
</div>
</div>
</body>
<.md>