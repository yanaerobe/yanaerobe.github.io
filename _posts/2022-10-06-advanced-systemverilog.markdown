---
title: WIP:进阶(System)Verilog笔记
date: 2022-10-6 22:09:50 +0100
categories: [乱抄, Coding]
tags: [Verilog]
---

## 格式规范

> 摘自[lowRISC Verilog Coding Style Guide](https://github.com/lowRISC/style-guides/blob/master/VerilogCodingStyle.md)
{: .prompt-info }

偏好`parameter`而非`define`，模块内基于其他`parameter`的参数使用`localparam`。

常量参数采用`UPPER_CASE`，而可配置的参数采用`UpperCamelCase`。

## bins

For `bins`, there's an interesting analogy: 

Imagine you in a Carnival playing some game like ringtoss: except that you're going to throw, like 10 balls, into 5 bins to win a stupid prize. 

If you manage your 10 chances into all 5 bins, that's called a 100% percent coverage. On the other hand, if 3 balls goes to the first bin, 3 the second and 4 the third, i.e., you miss the fourth and fifth bins, that's a coverage of 3/5=60%. 

Basically the concept of `bins`. 

Now in a more complex case, bins could be of various sizes: 

```verilog
//Markdown here doesn't support sv
  bins bin1 = {[0:2]};
  bins bin2 = {[3:4]};
  bins bin3 = {[5]};
  bins bin4 = {[6]};
  bins bin5 = {[7]};
//...
```

Now that the first bin is gigantic, 闭着眼都能扔进去, the second a little harder and others even harder. 

But this doesn't matter at all. What matters in coverage is the percentage of bins you hit, rather than neither bin sizes nor how many balls you threw in. 

That's `bins`. 
