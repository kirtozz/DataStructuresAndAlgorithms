## 各种小算法的汇总

> 作者时间精力实在有限，算法实现尽量全部使用C/C++。倘若有心者想使用Py、Java和Ruby等其他语言实现，完善此页。可pull requests此仓库,谨祝诸君共勉。

* 快速空降目录        
    <a href='#BinarySearch' >二分查找 Array.1</a>    
    <a href='#BubbleSort' >冒泡排序 BigO.1</a>     
    <a href='#SelectSort' >选择排序 BigO.2</a>    
    <a href='#InsertSort' >插入排序 BigO.3</a>     
    <a href='#StackInSequence' >LIFO 栈的顺序存储实现 SAQ.1</a>        
    <a href='#QueueInSequence' >FIFO 队列的顺序存储实现 SAQ.2</a>      
    
[代码优化实例与具体数据结构实战](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/OptimizeExps.md) 

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

void init(Stack *S, int a) // 初始化
{
	S->bottom = (ElemType *)malloc(a * sizeof(ElemType)); // 初始化内存
	S->top = S->bottom;									  // 栈空时，栈顶和栈底的指针相同。
	S->stacksize = a;									  // 记录栈的容量
}

void push(Stack *S, ElemType e) // 压栈
{
	if (S->top - S->bottom >= S->stacksize) // 栈满追栈加3个单位的内存
	{
		printf("栈满，追加内存\n");
		S->bottom = (ElemType *)realloc(S->bottom, (S->stacksize + 3) * sizeof(ElemType));
		S->top = S->bottom + S->stacksize;
		S->stacksize += 3;
	}
	*S->top = e;
	S->top++;
}

void pop(Stack *S) // 出栈
{
	if (S->bottom == S->top) // 栈空就提前结束
	{
		printf("栈空！程序结束");
		exit(0);
	}
	S->top--;
}

ElemType read(Stack *S) // 读取栈顶元素
{
	if (S->top == S->bottom)
	{
		printf("栈空！程序结束");
		exit(0);
	}
	return *(S->top - 1);
}

void ShowAll(Stack *S) // 遍历所有元素
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
	printf("栈顶的元素是%c\n", t);
	ShowAll(&S);
	return 0;
}
~~~

<span id="QueueInSequence">FIFO 队列的顺序存储实现</span>  
~~~
#include <stdio.h>
#include <stdlib.h>

#define MAX_QUEUE_SIZE 6
typedef char ElemType;
typedef struct queue
{
	ElemType Queue_array[MAX_QUEUE_SIZE]; // 数据部分，用数组
	int front;							  // 队首的位置
	int rear;							  // 队尾的位置
} Queue;

void init(Queue *Q) // 初始化
{
	Q->rear = 0;
	Q->front = 0;
}
void insert(Queue *Q, ElemType e) // 入队
{
	if ((Q->rear + 1) % MAX_QUEUE_SIZE == Q->front) // 若队满提前结束
	{
		printf("队满！结束程序");
		exit(0);
	}
	Q->Queue_array[Q->rear] = e;
	Q->rear = (Q->rear + 1) % MAX_QUEUE_SIZE; // 队尾取余来实现循环的逻辑结构
}
void del(Queue *Q) // 出队
{
	if (Q->front == Q->rear) // 若队空提前结束
	{
		printf("队空！结束程序");
		exit(0);
	}
	Q->front = (Q->front + 1) % MAX_QUEUE_SIZE;
}
ElemType read(Queue *Q) // 读取队首元素
{
	if (Q->front == Q->rear)
		exit(0);
	return Q->Queue_array[Q->front];
}
void ShowAll(Queue *Q) // 遍历所有元素
{
	int t = Q->front;
	int i = 0;
	while (t != Q->rear)
	{
		printf("第%d个数值为%c\n", i, Q->Queue_array[t]);
		i++;
		t = (t + 1) % MAX_QUEUE_SIZE;
	}
	printf("显示完毕\n");
}

int main()
{
	ElemType t;
	Queue Q;
	init(&Q);
	insert(&Q, 'A');
	insert(&Q, 'B');
	insert(&Q, 'C');
	insert(&Q, 'D');
	// insert(&Q, 'E');
	// insert(&Q, 'F');
	// insert(&Q, 'G');
	// insert(&Q, 'H');
	ShowAll(&Q);
	del(&Q);
	t = read(&Q);
	printf("队首的元素是%c\n", t);
	ShowAll(&Q);
	return 0;
}
~~~




