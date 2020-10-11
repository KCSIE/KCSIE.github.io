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


## Introduction

#### Concept

In computer science, algorithmic efficiency is a property of an algorithm which relates to the number of computational resources used by the algorithm. The algorithm efficiency is the time it takes to execute an algorithm, which is measured by the time it takes for the program based on the algorithm to run on the computer. An algorithm must be analyzed to determine its resource usage, and the efficiency of an algorithm can be measured based on usage of different resources. 

#### Measurement Method

There are usually two ways to measure the execution time of a program:

+ Ex-Post statistical method

+ Ex-Ante analytical estimation method

A program's runtime is characterized by its time and space complexity.

<img style="display: block; margin: 0 auto;" src="https://bkimg.cdn.bcebos.com/formula/f1efd43e838dc4e51938e9f3728d3241.svg" alt="" />

The above formula indicates that as the size of the problem n increases, the growth rate of the algorithm execution time is the same as the growth rate of f(n), called the asymptotic time complexity of the algorithm, referred to as the time complexity.

<img style="display: block; margin: 0 auto;" src="https://bkimg.cdn.bcebos.com/formula/6afccbcf4be4bc550afadbc806c062fd.svg" alt="" />

The above formula represents the spatial complexity. Space complexity can be a measure of the storage space required by an algorithm. If the auxiliary space required for the execution of the algorithm is a constant relative to the amount of input data, then the algorithm is said to work in-place.

#### Best, Worst & Average Cases

+ Not all inputs of a given size take the same time to run
+ Best case
  - Too optimistic, not likely to be representative
  - Useful when the best case has high probability of occurring
+ Worst case
  + The algorithm must perform at least that well, especially important for real-time applications

+ Average case
  + Typical behavior of the algorithm
  + First requires that we understand how the actual inputs to the program (and their costs) are distributed

For maximum efficiency we wish to minimize resource usage. However, different resources such as time and space complexity cannot be compared directly, so which of two algorithms is considered to be more efficient often depends on which measure of efficiency is considered most important. According to a vast amount of practical experience, we usually focus on the worst case efficiency when we evaluate an algorithm.



## Time Complexity & Asymptotic Notations

####  Big-Oh

Upper Bound (Big-Oh "O" notation):

+ Indicates the upper or highest growth rate that the algorithm can have

+ Definition: T(n)=O(f(n)),  if there exist two positive constants c and n0 such that T(n) <= cf(n) for all n > n0 

+ Example:  

  ```txt
  Suppose T(n) = c1n² + c2n, where c1 and c2 are positive. 
  Ans: 
  c1n² + c2n <= c1n² + c2n² <= (c1 + c2 )n² for all n > 1. 
  Then, T(n) <= cn² whenever n > n0 , for c = c1 + c2 and n0 = 1. Therefore, T(n) is in O(n²) by definition.
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-2.png" alt="" />

#### Big-Omega

Lower Bound (Big-Omega "Ω" notation):

+ Describe the least amount of a resource that an algorithm needs for some class of input

+ Definition: T(n)=Ω(g(n)),  if there exist two positive constants c and n0 such that T(n) >= cg(n) for all n > n0

+ Example:  

  ```txt
  Suppose T(n) = c1n² + c2n, where c1 and c2 are positive. 
  Ans: 
  c1n² + c2n >= c1n² for all n > 1. 
  Then, T(n) >= cn² for c = c1 and n0 = 1. 
  Therefore, T(n) is in Ω(n²) by the definition.
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-3.png" alt="" />

#### Big-Theta

"θ" notation:

+ When Big-Oh and Big-Omega coincide, we indicate this by using "θ" (Big-Theta) notation

+ Definition: An algorithm is said to be θ(h(n)) if it is in O(h(n)) and it is in Ω(h(n))

+ Example: 

  ```
  The sequential search algorithm is both in O(n) and in Ω(n) in the average case, we say it is θ(n) in the average case.
  ```

  

<img style="display: block; margin: 0 auto;" src="https://media.geeksforgeeks.org/wp-content/uploads/AlgoAnalysis-1.png" alt="" />

## Simplifying & Calculating Rules

#### How to deduce the Big-Oh?

1. Replace all additive constants in the runtime with the constant 1
2. In the modified run count function, only the highest order terms are retained
3. If the highest order term exists and is not 1, remove the constant multiplied by this term

#### Examples

+ Constant order

  ```
  int sum=0,n=0;
  sum=(1+n)*n/2;
  printf("%d",sum);
  /* Although f(n)=3, the time complexiy is O(1). */
  ```

+ Linear order 

  ```
  int i;
  for(i=0;i<n;i++)
  {
  	/* Perform n times with time complexity O(1). 
  	So the time complexiy is O(n). */
  }
  ```

+ Logarithmic order 

  ```
  int count=1;
  while(count<n)
  {
  	count=count*2;s
  	/* Break when it find 2^x=n (x=log₂n)
  	So the time complexiy is O(logn). */
  }
  ```

+ Quadratic order 

  ```
  int i,j;
  for(i=0;i<n;i++)
  {
  	for(j=0;j<n;j++)
  	{
  		/There are two layers of loop.
  		The inner time complexiy is O(n).
  		Recirculate n times.
          So the time complexiy is O(n²). */
  	}
  }
  ```

  ```
  int i,j;
  for(i=0;i<m;i++)
  {
  	for(j=0;j<n;j++)
  	{
  		/There are two layers of loop.
  		The inner time complexiy is O(n).
  		Recirculate m times.
          So the time complexiy is O(m*n). */
  	}
  }
  ```

  ```
  int i,j;
  for(i=0;i<n;i++)
  {
  	for(j=i;j<n;j++)
  	{
  		/When i=0, the inner loop executes n times,
  		when i=1, it executes n-1 times ...
  		when i=n-1, it executes 1 time.
  		The sum of execution's times is:
  		n+(n-1)+(n-2)+...+1=n(n+1)/2=n²/2+n/2.
          According to the rule of deduction,
          the time complexiy is O(n²). */
  	}
  }
  ```

+ Complex situation 

  ```
  n++;	/* Execute 1 time */
  function(n);	/* Execute n times */
  int i,j;
  for(i=0;i<n;i++)	/* Execute n² times */
  {
  	function(i);
  }
  for(i=0;i<n;i++)	/* Execute n(n+1)/2 times */
  {
  	for(j=i;j<n;j++)
  	{
  		/* f(n)=3/2n²+3/2n+1
          According to the rule of deduction,
          the time complexiy is O(n²). */
  	}
  }
  ```

#### Common Big-Oh of Time Complexity

| Order       | Name                                    | Example       |
| ----------- | --------------------------------------- | ------------- |
| O(1)        | constant                                | 12            |
| O(n)        | linear                                  | 2n+3          |
| O(n²)       | quadratic                               | 3n²+2n+1      |
| O(logn)     | logarithmic                             | 5log₂n+20     |
| O(nlogn)    | linearithmic, loglinear, or quasilinear | 2n+3nlog₂n+19 |
| O(n³)       | cubic                                   | 6n³+2n²+3n+4  |
| O(c^n), c>1 | exponential                             | 2^n           |

The time spent is in order of: 

O(1) < O(logn) < O(n) < O(nlogn) < 0(n²) < 0(n³) < 0(2^n) < O(n!) < O(n^n) 

<img style="display: block; margin: 0 auto;" src="https://upload-images.jianshu.io/upload_images/42676-bbe7324ed0878134.png?imageMogr2/auto-orient/strip|imageView2/2/w/819/format/webp" alt="" />



<img style="display: block; margin: 0 auto;" src="" alt="" />