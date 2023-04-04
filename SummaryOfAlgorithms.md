## 各种小算法的汇总

> 作者时间精力实在有限，算法实现尽量全部使用C/C++。倘若有心者想使用Py、Java和Ruby等其他语言实现，完善此页。可pull requests此仓库,谨祝诸君共勉。

* 快速空降目录
    <a href='#BinarySearch' >二分查找 Array.1</a>    
    <a href='#BubbleSort' >冒泡排序 BigO.1</a>     
    <a href='#SelectSort' >选择排序 BigO.2</a>    
    <a href='#InsertSort' >插入排序 BigO.3</a>     
    <a href='#StackInSequence' >LIFO 栈的顺序存储实现 SAQ.1</a>      
    <a href='#CorrectionOfStack' >基于栈的代码语法分析器 SAQ.2</a>   
    <a href='#QueueInSequence' >FIFO 队列的顺序存储实现 SAQ.3</a>      
    <a href='#PrinterOfQueue' >基于队列的打印机 SAQ.4</a>             




---

<span id="BinarySearch">二分查找</span>    
~~~
int binary_search(int arr[], int n, int search_value)
{
  int lower = 0;
  int upper = n - 1;
  int mid, temp;
  while (lower <= upper)
  {
    mid = (lower + upper) / 2;       //利用编程语言的向下取整
    temp = arr[mid];
    if (search_value == temp)
      return mid;
    else if (search_value < temp)
      upper = mid - 1;
    else
      lower = mid + 1;
  }
  return -1;
}
~~~

<span id="BubbleSort">冒泡排序</span>    
~~~
void bubble_sort(int arr[], int n)
{
  int i, t, flag = 0;         // flag是标志位
  while (flag != 1)
  {
    flag = 1;
    for (i = 0; i < n - 1; i++)
      if (arr[i] > arr[i + 1]) 
      {
        t = arr[i];           //两个变量交换需要临时变量存储中间值
        arr[i] = arr[i + 1];
        arr[i + 1] = t;
        flag = 0;
      }
    n--;
  }
}
~~~    

<span id="SelectSort">选择排序</span>   
~~~   
void select_sort(int arr[], int n)
{
  int i, j, t, MinIndex;
  for (i = 0; i < n - 1; i++)
  {
    MinIndex = i;                //“擂台主”  
    for (j = i + 1; j < n; j++)
    {
      if (arr[j] < arr[MinIndex])
        MinIndex = j;
    }
    if (MinIndex != i)
    {                           
      t = arr[i];
      arr[i] = arr[MinIndex];
      arr[MinIndex] = t;
    }
  }
}
~~~     

<span id="InsertSort">插入排序</span>   
~~~
void insert_sort(int arr[], int n)
{
  int i, j, temp;
  for (i = 1; i < n; i++)
  {
    temp = arr[i];
    j = i - 1;
    while (j >= 0)
      if (arr[j] > temp)
      {
        arr[j + 1] = arr[j];
        j = j - 1;
      }
      else
        break;
    arr[j + 1] = temp;
  }
}
~~~    

<span id="StackInSequence">LIFO 栈的顺序存储实现</span>
~~~
#include <stdio.h>
#include <stdlib.h> // malloc函数需要的库

typedef char ElemType;
typedef struct stack
{
	char *bottom;  //  栈不存在时值为NULL
	char *top;	   //  栈顶指针
	int stacksize; //  当前已分配空间，以元素为单位
} Stack;

void init(Stack *S, int a)
{
	S->bottom = (ElemType *)malloc(a * sizeof(ElemType)); // 初始化内存
	S->top = S->bottom;									  // 栈空时，栈顶和栈底的指针相同。
	S->stacksize = a;									  // 记录栈的容量
}

void push(Stack *S, ElemType e) // 压栈
{
	if (S->top - S->bottom >= S->stacksize) // 满追栈加3个单位的内存
		S->top = S->bottom + S->stacksize;
	{
		S->bottom = (ElemType *)realloc(S->bottom, (S->stacksize + 3) * sizeof(ElemType));
		S->stacksize += 3;
	}
	*S->top = e;
	S->top++;
}

void pop(Stack *S) // 出栈
{
	if (S->bottom == S->top) // 栈空就提前结束,可能有些不规范
		return;
	S->top--;
}

ElemType read(Stack *S) // 读取栈顶元素
{
	if (S->top == S->bottom)
		return -11111111; // 若栈空返回错误代码"-11111111"
	return *S->top;
}

void ShowAll(Stack *S)
{
	ElemType *p = S->top;
	int i = 0;
	while (S->bottom != p)
	{
		p--;
		printf("第%d个元素的值为%c\n", i, *p);
		i++;
	}
	printf("显示完毕\n");
}

int main() // 主函数演示功能
{
	Stack S;
	ElemType t;
	init(&S, 3);
	push(&S, 'A');
	push(&S, 'B');
	push(&S, 'C');
	push(&S, 'D');
	push(&S, 'E');
	push(&S, 'F');
	push(&S, 'G');
	ShowAll(&S);
	pop(&S);
	t = read(&S);
	printf("出栈元素是%c\n", t);
	pop(&S);
	ShowAll(&S);
	return 0;
}
~~~

<span id="CorrectionOfStack">基于栈的代码语法分析器</span>     
~~~

~~~


<span id="QueueInSequence">FIFO 队列的顺序存储实现</span>  
~~~

~~~

<span id="PrinterOfQueue">基于队列的打印机</span>     
~~~

~~~




