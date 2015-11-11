---
layout: post
title: 基于Cyclone 3的系统硬件设计
date: 2011-04-30 18:30
author: tglgg821
comments: true
categories: [Techniques]
---
&nbsp;
<p align="LEFT">一、背景</p>
<p align="LEFT">SOPC是个很时髦的概念，计划基于Cyclone3系列的FPGA芯片，使用软核NIOS Ii为核心，设计一个具有数字输入输出，AD采集和DA转换和串口的系统。</p>
<p align="LEFT">二、芯片选型</p>
<p align="LEFT">核心芯片选用Cyclone III系列的芯片。Cyclone III是ALTERA新推出的FPGA芯片。在这里选用EP3C25E144C7，封装是144 pin EQFP。</p>
<p align="LEFT">配置芯片选择了EPCS16SI16N，16M的。ALTERA的FPGA芯片可以设计成多种配置模式。有AS配置模式，AP配置模式，PS配置模式和FPP配置模式。在这里我选择了AS配置模式，就是串行配置模式。</p>
<p align="LEFT">JTAG配置中有一种模式是可以将数据保存再配置芯片里的，但是当时没选择，其实应该选的。应该是JTAG 和 AS Configuration 配置。</p>
<p align="LEFT">设计输入是+5V电源，电源转换芯片选用了HT7333，HT7325，HT7318，因为核心芯片需要+1.2V的电压，故在HT7318芯片后增加了一个电阻分压电路。HT73XX系列芯片是低功耗的低压差线性稳压器，因为以前用过，所以在这里选用。其实这几个芯片的选型是很冒失的。而且最后由于HT7318后的电阻分压电路无效，串接了一个二极管才成功。 而且HT73XX系列芯片的输出最大只有250mA，所以这个板子的电源部分设计是个失败。基本没做太多的考虑。</p>
<p align="LEFT">这里记一下稳压器LDO的四大要素：压差Dropout、噪音Noise、电源抑制比PSRR、静态电流Iq。</p>
<p align="LEFT">Ad选择了AD7888，这是一个SPI接口的AD采集芯片。</p>
<p align="LEFT">Da选择了MAX521，同样是一个SPI接口的DA转换芯片。</p>
<p align="LEFT">232串行芯片选择了MAX3222EWN，这个没什么可说的。</p>
<p align="LEFT">422穿行芯片选择了MAX3490，同样没什么可说的。</p>
<p align="LEFT">三、电路设计</p>
<p align="LEFT">该电路板采用了8层板的设计，其实现在想来最多6层就够了。</p>
<p align="LEFT">四、经验及教训</p>
<p align="LEFT">1、最愚蠢的事情是我把50MHz的晶振的封装选错了，太小，结果板子回来后发现无法焊接。最后只能半翘着焊接，不过最神奇的是板子最后竟然调通了。</p>
<p align="LEFT">2、电源部分的设计实在是个渣，连设计都算不上，随便选了三个稳压器就放上去了，最后还得需要加了个二极管才顺利的实现+1.2V的电压。</p>
<p align="LEFT">3、JTAG部分的电路应该当时再慎重一些，AS配置方式才是当时最好的选择。</p>
<p align="LEFT">五、改进建议</p>
<p align="LEFT">1、板子其实可以再稍微大点，布局如果安排的好的话，4层也许就能下来。</p>
<p align="LEFT">2、封装的选择一定要慎重，要努力做到一版成功。</p>
<p align="LEFT">3、芯片的周围最好还是要多加0.01uF的电容，该板上加的很少。</p>
<p align="LEFT">4、由于后来改用ACTEL芯片的原因，没有在这个板子的调试上花费太多时间，所以对CycloneIII系列芯片的特点摸的不是很清楚。如果后边有时间的话，最好还是能将其重新拾起来，好好的调试调试，摸一摸芯片的特性。</p>
