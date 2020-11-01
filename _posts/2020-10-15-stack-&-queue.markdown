---
layout: post
title: Stack & Queue
date: 2020-10-15 10:59:26 +0800
categories: Study
tags: Theory DataStructures
img: https://s1.ax1x.com/2020/11/01/BdxaPx.jpg
author: Reprint 转载
describe: 栈与队列 (Data Structures & Algorithm Analysis-3/数据结构与算法分析-3)
---

## 栈

### 1. 栈的简介

#### 1.1栈的特点

栈(Stack)是一种线性存储结构，它具有如下特点：

1. 栈中的数据元素遵守”先进后出"(First In Last Out)的原则，简称FILO结构。
2. 限定只能在栈顶进行插入和删除操作。

#### 1.2栈的相关概念

栈的相关概念：

1. 栈顶与栈底：允许元素插入与删除的一端称为栈顶，另一端称为栈底。
2. 压栈：栈的插入操作，叫做进栈，也称压栈、入栈。
3. 弹栈：栈的删除操作，也叫做出栈。

例如我们有一个存储整型元素的栈，我们依次压栈：{1,2,3}
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130013806989-121668995.png)

在压栈的过程中，栈顶的位置一直在”向上“移动，而栈底是固定不变的。
如果我们要把栈中的元素弹出来：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130013814661-295746330.png)

出栈的顺序为3、2、1 ，顺序与入栈时相反，这就是所谓的”先入后出“。
在弹栈的过程中，栈顶位置一直在”向下“移动，而栈底一直保持不变。

如果你玩过一种称为汉诺塔的益智玩具，你就会知道游戏中小圆盘的存取就是一种先进后出的顺序，一个圆柱就是一个栈：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130013821489-1542512229.png)

#### 1.3 栈的操作

栈的常用操作为：

1. 弹栈，通常命名为pop
2. 压栈，通常命名为push
3. 求栈的大小
4. 判断栈是否为空
5. 获取栈顶元素的值

#### 1.4 栈的存储结构

栈既然是一种线性结构，就能够以数组或链表（单向链表、双向链表或循环链表）作为底层数据结构。
本文我们以数组、单向链表为底层数据结构构建栈。

### 2. 基于数组的栈实现

当以数组为底层数据结构时，通常以数组头为栈底，数组头到数组尾为栈顶的生长方向：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130013928458-208656397.png)

#### 2.1 栈的抽象数据类型

栈提供了如上所述操作的相应接口。

```cpp
template<typename T>
class ArrayStack
{
public:
    ArrayStack(int s = 10);    //默认的栈容量为10
    ~ArrayStack();
 
public:
    T top();            //获取栈顶元素
    void push(T t);        //压栈操作
    T pop();            //弹栈操作
    bool isEmpty();        //判空操作
    int size();            //求栈的大小
 
private:
    int count;            //栈的元素数量
    int capacity;        //栈的容量
    T * array;            //底层为数组
};
```

1. count 为栈的元素数量，capacity为栈的容量，count<=capacity，当栈满的时候，count = capacity。
2. 本实现中不支持栈的动态扩容，栈满的时候无法再插入元素。栈的容量在定义栈的时候就需要指定，默认的栈容量为10。

#### 2.2 栈的具体实现

栈的实现还是相对简单的，很容易理解。这里就不再画蛇添足了。

```cpp
 /*栈的判空操作*/
template <typename T>
bool ArrayStack<T>::isEmpty()
{
     return count == 0; //栈元素为0时为栈空
};
 
/*返回栈的大小*/
 template <typename  T>
int ArrayStack<T>::size()
{
     return count;
};
 
/*插入元素*/
template <typename T>
void ArrayStack<T>::push(T t)
{
     if (count != capacity)    //先判断是否栈满
     {
         array[count++] = t;   
     }
};
 
/*弹栈*/
template <typename T>
T ArrayStack<T>::pop()
{
     if (count != 0)    //先判断是否是空栈
     {
         return array[--count];
     }
};
 
/*获取栈顶元素*/
template <typename T>
T ArrayStack<T>::top()
{
     if (count != 0)
     {
         return array[count - 1];
     }
};
 
```

#### 2.3 栈的代码测试

```cpp
int _tmain(int argc, _TCHAR* argv[])
{
    ArrayStack <int> p(5);
    for (int i = 0; i < 5; i++)
    {
        p.push(i);
    }
    cout << "栈的大小:"<<p.size() << endl;
    cout << "栈是否为空:"<<p.isEmpty() << endl;
    cout << "栈顶元素："<<p.top() << endl;
    cout << "依次出栈:" << endl;
    while (!p.isEmpty())
    {
        cout << p.pop() << endl;
    }
    getchar();
    return 0;
}
```

测试结果：

```cpp
栈的大小:5
栈是否为空:0
栈顶元素：4
依次出栈:
4
3
2
1
0
```

### 3. 基于单链表的栈

以链表为底层的数据结构时，以链表头为作为栈顶较为合适，这样方便节点的插入与删除。压栈产生的新节点将一直出现在链表的头部；
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130013944943-399164407.png)

#### 3.1 链表节点

```cpp
/*链表节点结构*/
template <typename T>
struct Node
{
    Node(T t) :value(t), next(nullptr){};
    Node() :next(nullptr){};
 
public:
    T value;
    Node<T>* next;
};
```

1. value:栈中元素的值
2. next:链表节点指针，指向直接后继

#### 3.2 栈的抽象数据类型

基于链表的栈提供的接口与基于数组的栈一致。

```cpp
/*栈的抽象数据结构*/
template <typename T>
class LinkStack
{
public:
     LinkStack();
     ~LinkStack();
public:
 
     bool isEmpty();
     int size();
     void push(T t);
     T pop();
     T top();
 
private:
 
     Node<T>* phead;
     int count;
};
```

#### 3.3 栈的具体实现

```cpp
/*返回栈的大小*/
template <typename T>
int LinkStack<T>::size()
{
     return count;
};
/*栈的判空操作*/
template <typename T>
bool LinkStack<T>::isEmpty()
{
     return count == 0;
};
/*插入元素*/
template<typename T>
void LinkStack<T>::push(T t)
{
     Node <T> *pnode = new  Node<T>(t);
     pnode->next = phead->next;
     phead->next = pnode;
     count++;
};
/*弹栈*/
template <typename T>
T LinkStack<T>::pop()
{
     if (phead->next != nullptr) //栈空判断
     {
         Node<T>* pdel = phead->next;
         phead->next = phead->next->next;
         T value = pdel->value;
         delete pdel;
         count--;
         return value;
     }
};
/*获取栈顶元素*/
template <typename T>
T LinkStack<T>::top()
{
    if (phead->next!=nullptr)
        return phead->next->value;
};
```

#### 3.4 栈的代码测试

```cpp
int _tmain(int argc, _TCHAR* argv[])
{
    LinkStack <string> lstack;
    lstack.push("hello");
    lstack.push("to");
    lstack.push("you！");
 
    cout << "栈的大小:" << lstack.size() << endl;
    cout <<"栈顶元素:"<< lstack.top() << endl;
 
    while (!lstack.isEmpty())
    {
        lstack.pop();
    }
 
    cout << "栈的大小:" << lstack.size() << endl;
 
    getchar();
    return 0;
}
```

测试结果：

```cpp
栈的大小:3
栈顶元素:you！
栈的大小:0
```

### 4. 栈的完整代码

#### 4.1 基于数组的栈

```c++
/* 基于数组的栈实现 */
# ifndef ARRAY_STACK_HPP
# define ARRAY_STACK_HPP

template<typename T>
class ArrayStack
{
public:
	ArrayStack(int s = 10);	//默认的栈容量为10
	~ArrayStack();

public:
	T top();			//获取栈顶元素
	void push(T t);		//压栈操作
	T pop();			//弹栈操作
	bool isEmpty();		//判空操作
	int size();			//求栈的大小

private:
	int count;			//栈的元素数量
	int capacity;		//栈的容量
	T * array;			//底层为数组
};

/*构造函数*/
template <typename T>
 ArrayStack<T>::ArrayStack(int s = 10)
	 :count(0), capacity(s), array(nullptr)
 {
	 array = new T[capacity];
 };

 /*析构函数*/
 template<typename T>
 ArrayStack<T>::~ArrayStack()
 {
	 if (array)
	 {
		 delete[]array;
		 array = nullptr;
	 }
 };

 /*栈的判空操作*/
 template <typename T>
 bool ArrayStack<T>::isEmpty()
 {
	 return count == 0; //栈元素为0时为栈空
 };

 /*返回栈的大小*/
 template <typename  T>
 int ArrayStack<T>::size()
 {
	 return count;
 };

 /*插入元素*/
 template <typename T>
void ArrayStack<T>::push(T t)
 {
	 if (count != capacity)	//先判断是否栈满
	 {
		 array[count++] = t;	
	 }
 };

/*弹栈*/
 template <typename T>
 T ArrayStack<T>::pop()
 {
	 if (count != 0)	//先判断是否是空栈
	 {
		 return array[--count];
	 }
 };

 /*获取栈顶元素*/
 template <typename T>
 T ArrayStack<T>::top()
 {
	 if (count != 0)
	 {
		 return array[count - 1];
	 }
 };

# endif 
```

#### 4.2 基于单链表的栈

```c++
/* 基于单链表的栈实现 */
# ifndef SINGLE_LIST_HXX
# define SINGLE_LIST_HXX

//节点结构
template <typename T>
class Node
{
public :
	T _value;
	Node* _next;
public:
	Node() = default;
	Node(T value, Node * next)
		: _value(value), _next(next){}
};

//单链表
template <typename T>
class SingleLink
{
public:
	typedef Node<T>*  pointer;
	SingleLink();
	~SingleLink();

	int size();						 //获取长度
	bool isEmpty();					 //判空

	Node<T>* insert(int index, T t); //在指定位置进行插入
	Node<T>* insert_head(T t);		 //在链表头进行插入
	Node<T>* insert_last(T t);		 //在链表尾进行插入

	Node<T>*  del(int index);		 //在指定位置进行删除
	Node<T>*  delete_head();		 //删除链表头
	Node<T>*  delete_last();		 //删除链表尾

	T get(int index);			     //获取指定位置的元素
	T get_head();					 //获取链表头元素
	T get_last();					 //获取链表尾元素

	Node<T>* getHead();				 //获取链表头节点

private :
	int count;
	Node<T> * phead;				 

private :
	Node<T> * getNode(int index);	  //获取指定位置的节点
};

//默认构造函数
template <typename T>
SingleLink<T>::SingleLink()
:count(0), phead(nullptr)
{
	//创建头节点
	phead = new Node<T>();
	phead->_next = nullptr;
};

/* 返回指定索引的前一个位置节点，若链表为空，则返回头节点 */
template <typename T>
Node<T>* SingleLink<T>::getNode(int index)
{
	if (index > count||index < 0 )
		return nullptr;
	int temp = 0;
	Node<T>* preNode = phead;
	while (temp < index)
	{
		temp++;
		preNode = preNode->_next;
	}
	return preNode;
}

/* 析构函数 */
template <typename T>
SingleLink<T>::~SingleLink()
{
	Node<T>* pNode = phead->_next;
	while (nullptr != pNode)
	{
		Node<T>* temp = pNode;
		pNode = pNode->_next;
		delete temp;
	}
	//进行销毁
};

//返回链表的大小
template <typename T>
int SingleLink<T>::size()
{
	return count;
};

//链表判空
template <typename T>
bool SingleLink<T>::isEmpty()
{
	return count==0;
};

template<typename T>
Node<T>* SingleLink<T>::getHead()
{
	return phead->_next;
}

/* 在指定位置插入新节点 */
template <typename T>
Node<T>* SingleLink<T>::insert(int index, T t)
{
	Node<T> * preNode = getNode(index);
	if (preNode)
	{
		Node<T> *newNode = new Node<T>(t,preNode->_next); //构建新节点，构建时指明节点的next节点
		preNode->_next = newNode;
		count++;
		return newNode;
	}
	return nullptr;
};

/* 从头部插入 */
template <typename T>
Node<T>* SingleLink<T>::insert_head(T t)
{
	return insert(0, t);
};

/* 从尾部进行插入 */
template <typename T>
Node<T>* SingleLink<T>::insert_last(T t)
{
	return insert(count, t);
};

/* 删除链表指定位置元素 */
template <typename T>
Node<T>* SingleLink<T>::del(int index)
{
	if (isEmpty())
		return nullptr;
	Node<T>* ptrNode = getNode(index);
	Node<T>* delNode = ptrNode->_next;
	ptrNode->_next = delNode->_next;
	count--;
	delete delNode;
	return ptrNode->_next;
};

/* 删除头节点 */
template<typename T>
Node<T>* SingleLink<T>::delete_head()
{
	return del(0);
};

/* 删除尾节点 */
template<typename T>
Node<T>*SingleLink<T>::delete_last()
{
	return del(count);
};

# endif
```

### 转载来源

```
作者：melonstreet
出处：http://www.cnblogs.com/QG-whz/p/5170418.html
```



## 队列

### 1. 队列简介

#### 1.1 队列的特点

队列（Queue）与栈一样，是一种线性存储结构，它具有如下特点：

1. 队列中的数据元素遵循“先进先出”（First In First Out）的原则，简称FIFO结构。
2. 在队尾添加元素，在队头添加元素。

#### 1.2 队列的相关概念

队列的相关概念：

1. 队头与队尾： 允许元素插入的一端称为队尾，允许元素删除的一端称为队头。
2. 入队：队列的插入操作。
3. 出队：队列的删除操作。

例如我们有一个存储整型元素的队列，我们依次入队：{1，2，3}
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130151820974-712348880.png)

添加元素时，元素只能从队尾一端进入队列，也即是2只能跟在1后面，3只能跟在2后面。
如果队列中的元素要出队：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130151830318-592472607.png)

元素只能从队首出队列，出队列的顺序为：1、2、3，与入队时的顺序一致，这就是所谓的“先进先出”。

#### 1.3 队列的操作

队列通常提供的操作：

1. 入队： 通常命名为push()
2. 出队： 通常命名为pop()
3. 求队列中元素个数
4. 判断队列是否为空
5. 获取队首元素

#### 1.4 队列的存储结构

队列与栈一样是一种线性结构，因此以常见的线性表如数组、链表作为底层的数据结构。
本文中，我们以数组、链表为底层数据结构构建队列。

### 2.基于数组的循环队列实现

以数组作为底层数据结构时，一般讲队列实现为**循环队列**。这是因为队列在顺序存储上的不足：每次从数组头部删除元素（出队）后，需要将头部以后的所有元素往前移动一个位置，这是一个时间复杂度为O（n）的操作：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130152004193-1945216114.png)

可能有人说，把队首标志往后移动不就不用移动元素了吗？的确，但那样会造成数组空间的“流失”。
我们希望队列的插入与删除操作都是O(1)的时间复杂度，同时不会造成数组空间的浪费，我们应该使用循环队列。
所谓的循环队列，可以把数组看出一个首尾相连的圆环，删除元素时将队首标志往后移动，添加元素时若数组尾部已经没有空间，则考虑数组头部的空间是否空闲，如果是，则在数组头部进行插入。
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130152048146-364086587.png)

那么我们如何判断队列是空队列还是已满呢？

1. 栈空： 队首标志=队尾标志时，表示栈空，即红绿两个标志在图中重叠时为栈空。
2. 栈满 : 队尾+1 = 队首时，表示栈空。图三最下面的队列即为一个满队列。尽管还有一个空位，我们不存储元素。

#### 2.1 循环队列的抽象数据类型

```cpp
template <typename T>
class LoopQueue
{
public:
    LoopQueue(int c = 10);
    ~LoopQueue();
public:
    bool isEmpty();        //队列的判空
    int size();            //队列的大小
    bool push(T t);        //入队列
    bool pop();            //出队列
    T front();            //队首元素
 
private:
    int capacity;
    int begin;
    int end;
    T*  queue;
};
```

1. begin：队首标志
2. end：队尾标志
3. capacity：数组容量
4. queue：数组

#### 2.2 队列的具体实现

队列的操作非常简单，这里不再多说

```cpp
template<typename T>
LoopQueue<T>::LoopQueue(int c = 10)
: capacity(c), begin(0), end(0), queue(nullptr)
{
    queue = new T[capacity];
};
 
template<typename T>
LoopQueue<T>::~LoopQueue()
{
    delete[]queue;
}
 
template <typename T>
bool LoopQueue<T>::isEmpty()
{
    if (begin == end)
        return true;
    return false;
};
 
template<typename T>
int LoopQueue<T>::size()
{
    return (end-begin+capacity)%capacity; //计算队列长度
};
 
template<typename T>
bool LoopQueue<T>::push(T t)
{
    if (end + 1 % capacity == begin) //判断队列是否已满
    {
        return false;
    }
    queue[end] = t;
    end = (end + 1) % capacity;
    return true;
};
 
template <typename T>
bool LoopQueue<T>::pop()
{
    if (end == begin) //判断队列是否为空
    {
        return false;
    }
    begin = (begin + 1) % capacity;
    return true;
};
 
template <typename T>
T LoopQueue<T>::front()
{
    if (end == begin)
    {
        return false;
    }
    return queue[begin];
};
```

#### 2.3 循环队列代码测试

```cpp
int main()
{
    LoopQueue<string> queue(6);
    queue.push("one");
    queue.push("two");
    queue.push("three");
    queue.push("four");
    queue.push("five");
    cout << "队列长度" << queue.size() << endl;
    while (!queue.isEmpty())
    {
        cout << queue.front() << endl;
        queue.pop();
    }
    getchar();
    return 0;
 
}
```

测试结果：

```cpp
队列长度5
one
two
three
four
five
```

### 3. 链队列

链队列是基于链表实现的队列，它不存在数组的O（n）的元素移动问题或空间浪费问题。我们所要确定的就是链表哪头做队首，哪头做队尾。
显然我们应该以链表头部为队首，链表尾部为队尾。存储一个指向队尾的指针，方便从链表尾插入元素；使用带头节点的链表，方便从链表头删除元素。
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160130152133068-1288144578.png)

#### 3.1 链表节点

```cpp
template<typename T>
struct Node
{
    Node(T t) :value(t), next(nullptr){}
    Node() = default;
 
    T value;
    Node<T> * next;
};
```

1. vaule : 链表节点的值
2. next : 指针，指向下一个节点

#### 3.2 队列的抽象数据类型

链队列提供的接口与循环队列一致

```cpp
template<typename T>
class LinkQueue
{
public:
    LinkQueue();
    ~LinkQueue();
 
    bool isEmpty();
    int size();
    bool pop();
    void push(T t);
    T front();
 
private:
    Node<T>* phead;
    Node<T>* pend;
    int count;
};
```

#### 3.3 队列的具体实现

```cpp
template<typename T>
LinkQueue<T>::LinkQueue()
    :phead(nullptr),pend(nullptr),count(0)
{
    phead = new Node<T>();
    pend = phead;
    count = 0;
};
 
template <typename T>
LinkQueue<T>::~LinkQueue()
{
    while (phead->next != nullptr)
    {
        Node<T> * pnode = phead;
        phead = phead->next;
    }
};
 
template <typename T>
bool LinkQueue<T>:: isEmpty()
{
    return count==0;
};
 
template <typename T>
int LinkQueue<T>::size()
{
    return count;
};
 
//在队尾插入
template <typename T>
void LinkQueue<T>::push(T t)
{
    Node<T>* pnode = new Node<T>(t);
    pend->next = pnode;
    pend = pnode;
    count++;
};
 
//在队首弹出
template <typename T>
bool LinkQueue<T>::pop()
{
    if (count == 0)
        return false;
    Node<T>* pnode = phead->next;
    phead->next = phead->next->next;
    delete pnode;
    count--;
    return true;
};
 
//获取队首元素
template<typename T>
T LinkQueue<T>::front()
{
    return phead->next->value;
};
```

#### 3.4 队列的代码测试

```cpp
int _tmain(int argc, _TCHAR* argv[])
{
    LinkQueue<string> lqueue;
    lqueue.push("one");
    lqueue.push("two");
    lqueue.push("three");
    lqueue.push("four");
    lqueue.push("five");
    cout << "队列的大小" << lqueue.size() << endl;
    while (!lqueue.isEmpty())
    {
        cout << lqueue.front() << endl;
        lqueue.pop();
    }
    getchar();
    return 0;
}
```

运行结果：

```cpp
队列的大小5
one
two
three
four
five
```

### 4. 队列的完整代码

#### 4.1 循环队列

```c++
/* 循环队列 */
# ifndef LOOP_QUEUE_HPP
# define LOPP_QUEUE_HPP

template <typename T>
class LoopQueue
{
public:
	LoopQueue(int c = 10);
	~LoopQueue();
public:
	bool isEmpty();		//队列的判空
	int size();			//队列的大小
	bool push(T t);		//入队列
	bool pop();			//出队列
	T front();			//队首元素
private:
	int capacity;
	int begin;
	int end;
	T*  queue;
};

template<typename T>
LoopQueue<T>::LoopQueue(int c = 10) : capacity(c), begin(0), end(0), queue(nullptr)
{
	queue = new T[capacity];
};

template<typename T>
LoopQueue<T>::~LoopQueue()
{
	delete[]queue;
}

template <typename T>
bool LoopQueue<T>::isEmpty()
{
	if (begin == end)
		return true;
	return false;
};

template<typename T>
int LoopQueue<T>::size()
{
	return (end-begin+capacity)%capacity; //计算队列长度
};

template<typename T>
bool LoopQueue<T>::push(T t)
{
	if (end + 1 % capacity == begin) //判断队列是否已满
	{
		return false;
	}
	queue[end] = t;
	end = (end + 1) % capacity;
	return true;
};

template <typename T> 
bool LoopQueue<T>::pop()
{
	if (end == begin) //判断队列是否为空
	{
		return false;
	}
	begin = (begin + 1) % capacity;
	return true;
};

template <typename T>
T LoopQueue<T>::front()
{
	if (end == begin)
	{
		return false;
	}
	return queue[begin];
};

# endif
```

#### 4.2 链队列

```c++
/* 基于链表实现的队列 */
# ifndef LINK_QUEUE_HPP
# define LINK_QUEUE_HPP

template<typename T>
struct Node
{
	Node(T t) :value(t), next(nullptr){}
	Node() = default;

	T value;
	Node<T> * next;
};

template<typename T>
class LinkQueue
{
public:
	LinkQueue();
	~LinkQueue();

	bool isEmpty();
	int size();
	bool pop();
	void push(T t);
	T front();
private:
	Node<T>* phead;
	Node<T>* pend;
	int count;
};

template<typename T>
LinkQueue<T>::LinkQueue() :phead(nullptr),pend(nullptr),count(0)
{
	phead = new Node<T>();
	pend = phead;
	count = 0;
};

template <typename T>
LinkQueue<T>::~LinkQueue()
{
	while (phead->next != nullptr)
	{
		Node<T> * pnode = phead;
		phead = phead->next;
	}
};

template <typename T>
bool LinkQueue<T>:: isEmpty()
{
	return count==0;
};

template <typename T>
int LinkQueue<T>::size()
{
	return count;
};

//在队尾插入
template <typename T>
void LinkQueue<T>::push(T t)
{
	Node<T>* pnode = new Node<T>(t);
	pend->next = pnode;
	pend = pnode;
	count++;
};

//在队首弹出
template <typename T>
bool LinkQueue<T>::pop()
{
	if (count == 0)
		return false;
	Node<T>* pnode = phead->next;
	phead->next = phead->next->next;
	delete pnode;
	count--;
	return true;
};

//获取队首元素
template<typename T>
T LinkQueue<T>::front()
{
	return phead->next->value;
};

# endif
```

### 转载来源

```
作者：melonstreet
出处：http://www.cnblogs.com/QG-whz/p/5171123.html#_label3_0
```


