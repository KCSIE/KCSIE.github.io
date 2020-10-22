---
layout: post
title: Algorithm Efficiency
date: 2020-09-28 12:03:42 +0800
categories: Study
tags: Theory AlgorithmAnalysis
img: https://s1.ax1x.com/2020/10/11/0cMdFP.png
author: KCSIE
describe: 算法效率 (Data Structures & Algorithm Analysis-1/数据结构与算法分析-1)
---



## 导论

#### 概念

在计算机科学中，算法效率是算法的一种属性，它与算法使用的计算资源数量有关。算法效率是指执行一个算法所需的时间，它是由基于该算法的程序在计算机上运行所需的时间来衡量的。一个算法必须经过分析才能确定其资源使用情况，可以根据不同资源的使用情况来衡量算法的效率。

#### 度量方法

度量一个程序的执行时间通常有两种方法：

+ 事后统计方法

+ 事前分析估算方法

度量一个程序运行时间的方式通过时间复杂度和空间复杂度来表征。

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/12/0WMck9.png" alt="" />

上式表示随问题规模n的增大，算法执行时间的增长率和f(n)的增长率相同，称作算法的渐近时间复杂度，简称时间复杂度。

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/12/0WMyTJ.png" alt="" />

上式表示空间复杂度。空间复杂度可以作为算法所需存储空间的量度。若额外空间相对于输入数据量来说是常数，则称此算法为原地工作，空间复杂度为O(1)。

#### 最好，最坏和平均情况

+ 并非所有给定大小的输入都需要相同的运行时间
+ 最好情况
  - 太过乐观，不可能具有代表性
  - 当最好的情况发生的概率很高时有用
+ 最坏情况
  + 算法至少要有最坏情况这么好的性能，这对于实时应用来说尤其重要

+ 平均情况
  + 算法的典型表现
  + 首先需要我们了解计划的实际投入（及其成本）是如何分配的

为了获得最大的效率，我们希望尽量减少资源的使用。然而，不同的资源如时间和空间复杂度是无法直接比较的，所以两种算法中哪种被认为更有效率，往往取决于哪种效率的衡量标准被认为是最重要的。根据大量的实践经验，我们在评估一个算法时，通常会关注最坏情况下的效率。



## 时间复杂度与渐变符号

####  大O

上限(Big-Oh "O" 符号):

+ 表示该算法可以拥有的上限或最高增长率

+ 定义: 对所有n > n₀而言，如果存在两个正常数c和n₀，使T(n)<= cf(n)，有T(n)=O(f(n))

+ 例子:  

  ```txt
  假设 T(n) = c₁n² + c₂n, c₁和c₂是正的。
  答: 
  对所有n > 1有c₁n² + c₂n <= c₁n² + c₂n² <= (c₁ + c₂)n² 
  然后, 每当n>n₀时，对于c=c₁+c₂且n₀=1时有T(n) <= cn² 
  所以, T(n)上限为O(n²)
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-2.png" alt="" />

#### 大Omega

下限 (Big-Omega "Ω" 符号):

+ 描述算法对某类输入所需资源的最小量

+ 定义: 对于所有的n>n₀而言，如果存在两个正常数c和n₀，使T(n)>=cg(n)，有T(n)=Ω(g(n))

+ 例子:  

  ```txt
  假设 T(n) = c₁n² + c₂n, c₁和c₂是正的。
  答: 
  对所有n > 1有c₁n² + c₂n >= c₁n²  
  然后, c = c₁且n₀ = 1时有T(n) >= cn² 
  所以, T(n)下限为Ω(n²) 
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-3.png" alt="" />

#### 大Theta

"θ" 符号:

+ 当Big-Oh和Big-Omega重合时，我们用 "θ "(大Theta)来表示

+ 定义: 如果一个算法在O(h(n)中，并且它也在Ω(h(n)中，则称它是θ(h(n))

+ 例子: 

  ```
  顺序搜索算法既在O(n)，又在Ω(n)的平均情况下，我们说它在平均情况下是θ(n)。
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-1.png" alt="" />





## 化简与计算规则

#### 如何推导大O阶的时间复杂度?

1. 用常数1取代运行时间中所有加法常数
2. 在修改后的运行次数函数中，只保留最高阶项
3. 如果最高阶项存在且不是1，则去除与这个项相乘的常数

#### 例子

+ 常数阶

  ```
  int sum=0,n=0;
  sum=(1+n)*n/2;
  printf("%d",sum);
  /*尽管f(n)=3，时间复杂度是O(1)。*/
  ```

+ 线性阶 

  ```
  int i;
  for(i=0;i<n;i++)
  {
  	/* 执行了n次时间复杂度为O(1)的程序步骤， 
  	所以时间复杂度为O(n)。*/
  }
  ```

+ 对数阶

  ```
  int count=1;
  while(count<n)
  {
  	count=count*2;s
  	/* 当找到2^x=n (x=log₂n)时退出循环，
  	所以时间复杂度为O(logn)。*/
  }
  ```

+ 平方阶 

  ```
  int i,j;
  for(i=0;i<n;i++)
  {
  	for(j=0;j<n;j++)
  	{
  		/* 有两层循环，
  		内层的时间复杂度为O(n)，
  		又循环了n次，
          所以时间复杂度为O(n²)。*/
  	}
  }
  ```

  ```
  int i,j;
  for(i=0;i<m;i++)
  {
  	for(j=0;j<n;j++)
  	{
  		/* 有两层循环，
  		内层的时间复杂度为O(n)，
  		又循环了m次，
          所以时间复杂度为O(m*n)。*/
  	}
  }
  ```

  ```
  int i,j;
  for(i=0;i<n;i++)
  {
  	for(j=i;j<n;j++)
  	{
  		/当i=0，内层循环执行了n次，
  		当i=1，执行了n-1次 ...
  		当i=n-1，执行了1次。
  		执行次数的和为:
  		n+(n-1)+(n-2)+...+1=n(n+1)/2=n²/2+n/2.
          根据推导规则
          时间复杂度为O(n²)。*/
  	}
  }
  ```

+ 复杂情况

  ```
  n++;	/* 执行1次 */
  function(n);	/* 执行n次 */
  int i,j;
  for(i=0;i<n;i++)	/* 执行n²次 */
  {
  	function(i);
  }
  for(i=0;i<n;i++)	/* 执行n(n+1)/2次 */
  {
  	for(j=i;j<n;j++)
  	{
  		/* f(n)=3/2n²+3/2n+1
          根据推导规则
          时间复杂度为O(n²)。 */
  	}
  }
  ```

#### 常见的时间复杂度

| 阶          | 非正式术语 | 例子          |
| ----------- | ---------- | ------------- |
| O(1)        | 常数阶     | 12            |
| O(n)        | 线性阶     | 2n+3          |
| O(n²)       | 平方阶     | 3n²+2n+1      |
| O(logn)     | 对数阶     | 5log₂n+20     |
| O(nlogn)    | nlogn阶    | 2n+3nlog₂n+19 |
| O(n³)       | 立方阶     | 6n³+2n²+3n+4  |
| O(c^n), c>1 | 指数阶     | 2^n           |

时间复杂度所耗费的时间从小到大依次为: 

O(1) < O(logn) < O(n) < O(nlogn) < 0(n²) < 0(n³) < 0(2^n) < O(n!) < O(n^n) 

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/12/0WQp7Q.jpg" alt="" />

<img style="display: block; margin: 0 auto;" src="" alt="" />