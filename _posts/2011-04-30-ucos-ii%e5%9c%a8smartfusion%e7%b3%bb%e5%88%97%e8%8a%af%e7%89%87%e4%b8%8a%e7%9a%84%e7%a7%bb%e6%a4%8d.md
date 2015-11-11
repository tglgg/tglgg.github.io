---
layout: post
title: UCOS-II在Smartfusion系列芯片上的移植
date: 2011-04-30 01:03
author: tglgg821
comments: true
categories: [Techniques]
---
<p align="LEFT">一、背景</p>
<p align="LEFT">选择UCOS-II应用在Smarfusion系列芯片为核心的系统上，主要有以下几点考虑。</p>
<p align="LEFT">1、开源。</p>
<p align="LEFT">2、之前的移植实例多，可借鉴的东西较多。</p>
<p align="LEFT">3、网上，以及其他来源的评价还比较不错。</p>
<p align="LEFT">二、移植过程</p>
<p align="LEFT">Smartfusion系列芯片中内嵌 ARM Cortex-M3的内核，这样在Micrium的网站上有完整的例程，但是即使这样，还是出现了不少问题，当然最后都一一解决了。</p>
<p align="LEFT">移植过程如下，首先我参考了周立功的ARM 7的那本书，里面有移植UCOS-II 的部分，主要是对os_cpu.c、os_cpu_c.h和os_cpu_a.asm这三个文件进行修改，在这个过程中我查阅了ARM网站上关于CORTEX M3的资料，从arm7往cortex m3移植的参考手册，GNU汇编编译器的手册，等等许多相关的资料进行修改，同时我参考第二版的《ucos嵌入式系统》进行测试，最终完成。在此过程中硬件平台选用ACTEL公司自己的AVAL-KIT评估板。</p>
<p align="LEFT">三、问题记录</p>
<p align="LEFT">1、所有的文件后缀名必须小写，否则编译无法通过。</p>
<p align="LEFT">2、GNU编译器辨认的汇编文件后缀名为*.s。</p>
<p align="LEFT">2、GNU的汇编编译器在编译汇编语言时，需要对每一个函数进行声明，我就是不知道这一点，所以老是跳到HardFault_Handler这个向量上。</p>
<p align="LEFT">3、我开始的时候用的是2.52的版本，不知道为什么老是卡在Start Hang这个死循环上，没办法进行下去，就更换了2.86版本的，后来就好了。</p>
<p align="LEFT">4、更改PendSV_Handler向量名称，这样才能进行正常的上下文切换。</p>
<p align="LEFT">5、更改SysTick_Handler向量名称，才产生了正常的节拍中断。</p>
<p align="LEFT">6、保护临界段的方式选择第三种。周立功提供的第四种中断方式并不好，我在测试过程中出现了程序跑飞的现象。</p>
<p align="LEFT">基本就这些了，大概改完下来花了两个礼拜左右，</p>
<p align="LEFT">四、经验总结</p>
<p align="LEFT">这是第一次真正意义上的移植嵌入式系统，虽然比较简单，但是也从中学到了不少东西。 在后面的嵌入式系统编程中应该有很大的益处。</p>
<p align="LEFT">1、内核的调度机制，不用选择最复杂和最完善的，而应该选择最适合所选用的硬件平台和应用需求。</p>
<p align="LEFT">应用程序的编写会在下一步的工作中进行大量的应用，这到时候再进行进一步的总结。</p>
