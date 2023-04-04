## 用栈和队列打造优雅的代码    

现在我们要学习两种新的数据结构：栈和队列。其实它们并不陌生，栈和队列本质还是数组，只不过有一些限制。但正是这些**限制**让它们变得如此优雅。栈和队列是抽象数据类型，大多数编程语言中没有内置，需要自行实现。        

具体来说，栈和队列是处理**临时数据**的优雅方法，你可以把临时数据想象成银行里的叫号，在客户排队到本人的时候，这个号码此前的所有号码都可以扔掉，无需保存这些信息。临时数据是那些在处理后就不再重要的数据，用过之后即可丢弃。    

栈和队列正是处理这种临时数据的数据结构。不过它们对数据的顺序有着特别的要求。    

- [栈](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)

栈相比于数组的3个限制：    
- [ ] 数据只能从**栈末**插入。  
- [ ] 数据只能从**栈末**删除。  
- [ ] 只能读取栈的**最后**一个元素。    

总结概括上面的特点就是——后进先出（[LIFO](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)）。可以理解成叠盘子，我们操作盘子只能移动最上面的盘子。    
栈的开头叫**栈尾**，栈的末尾称为**栈顶**。    
向栈插入新值叫**压栈**，从栈顶移除元素称为**出栈**。   


![SAQ1.png](/pictures/SAQ1.png "栈的示意图")    

~~~
typedef char ElemType;
typedef struct stack
{
	ElemType *bottom;           //  栈不存在时值为NULL
	ElemType *top;	            //  栈顶指针
	int stacksize;	            //  当前已分配空间，以元素为单位
} Stack;

void init(Stack *) {}           // 初始化

void push(Stack *, ElemType) {} // 压栈

void pop(Stack *) {}            // 出栈

ElemType read(Stack *) {}       // 读取栈顶元素

void ShowAll(Stack *){}         //遍历所有元素
~~~

_既然栈是一个受限制的数组，那么数组就可以胜任栈的所有工作，那么栈又有什么优势呢？_

首先，使用受限数据结构可以避免潜在的错误，栈无法移除栈顶之外的元素，所以使用栈可以强制从栈顶移除元素。    
其次，像栈这样的数据结构为解决问题提供了一种新的思维方式。LIFO方法可用于解决各种问题，这里有个[代码语法分析器实战](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)。    



---

- [队列](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)     

队列相比于数组也有3个限制：    
- [ ] 数据只能插入队列**末尾**（与栈一样）。  
- [ ] 只能从队列**前端**删除数据（与栈相反）。  
- [ ] 只能读取队列的**第一个**数据（与栈相反）。    

这就是队列的先进先出（[FIFO](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)）。可以理解成叠盘子，我们操作盘子只能移动最上面的盘子。    

向队列插入新值叫**入队**，从前端移除元素称为**出队**。   


![SAQ2.png](/pictures/SAQ2.png "栈的示意图")    

~~~
typedef char ElemType;
typedef struct queue
{
	ElemType Queue_array[]; 	   // 数据部分，用数组
	int front;					   // 队首的位置
	int rear;					   // 队尾的位置
} Queue;

void init(Queue *) {} // 初始化

void insert(Queue *, ElemType) {} // 入队

void pop(Queue *) {} 			  // 出队

ElemType read(Queue *) {} 		  // 读取队首元素

void ShowAll(Queue *) {} 	      // 遍历所有元素
~~~

队列在很多应用中很常见，比如[打印机](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)的打印队列和网络应用中的后台任务。   
队列还是处理异步请求的完美工具，他们可以确保按顺序处理请求，队列也常用来模拟现实世界中需要按顺序处理时间的场景，比如飞机等待起飞或者病人看诊等。