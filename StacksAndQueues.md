## 用栈和队列打造优雅的代码    

现在我们要学习两种新的数据结构：栈和队列。其实它们并不陌生，栈和队列本质还是数组，只不过有一些限制。但正是这些**限制**让它们变得如此优雅。栈和队列是抽象数据类型，大多数编程语言中没有内置，需要自行实现。        

具体来说，栈和队列是处理**临时数据**的优雅方法，你可以把临时数据想象成银行里的叫号，在客户排队到本人的时候，这个号码此前的所有号码都可以扔掉，无需保存这些信息。临时数据是那些在处理后就不再重要的数据，用过之后即可丢弃。    

栈和队列正是处理这种临时数据的数据结构。不过它们对数据的顺序有着特别的要求。    

- [栈](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)

栈相比于数组的3个限制：    
- [ ] 数据只能从栈末插入。  
- [ ] 数据只能从栈末删除。  
- [ ] 只能读取栈的最后一个元素。    

总结概括上面的特点就是——后进先出（[LIFO](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)）。可以理解成叠盘子，我们操作盘子只能移动最上面的盘子。    
栈的开头叫**栈尾**，栈的末尾称为**栈顶**。    
向栈插入新值叫**压栈**，从栈顶移除元素称为**出栈**。   


![SAQ1.png](/pictures/SAQ1.png "栈的示意图")    

~~~
typedef struct stack
{   
	char  *bottom;    //  栈不存在时值为NULL  
	char  *top;       //  栈顶指针  
	int   stacksize ;     //  当前已分配空间，以元素为单位  
}Stack ;

void init(Stack *S){}      //初始化

void push(Stack *S,char *a){}    //压栈

void pop(Stack *S,char *a){}     //出栈

void read(Stack *S,char *a){}    //读取栈顶元素
~~~

_既然栈是一个受限制的数组，那么数组就可以胜任栈的所有工作，那么栈又有什么优势呢？_

首先，使用受限数据结构可以避免潜在的错误，栈无法移除栈顶之外的元素，所以使用栈可以强制从栈顶移除元素。    
其次，像栈这样的数据结构为解决问题提供了一种新的思维方式。LIFO方法可用于解决各种问题，这里有个[代码语法分析器实战](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)。    



---

- [队列](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)     