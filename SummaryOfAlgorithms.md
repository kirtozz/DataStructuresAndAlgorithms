## 各种小算法的汇总

> 作者时间精力实在有限，算法实现尽量全部使用C/C++。倘若有心者想使用Py、Java和Ruby等其他语言实现，完善此页。可pull requests此仓库,谨祝诸君共勉。

<a href='#BinarySearch' >二分查找 Array.1</a>
<a href='#BubbleSort' >冒泡排序 BigO.1</a>



<span id="BinarySearch">二分查找</span>
~~~
int binary_search(int arr[], int n, int search_value)
{
    int lower = 0;
    int upper = n - 1;
    int mid, temp;
    while (lower <= upper)
    {
        mid = (lower + upper) / 2;
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
void bubble_sort(int arr[],int n)
{
    int i,t,flag=0;    //flag是标志位
    while(flag!=1)
        {
            flag=1;
            for(i=0;i<n-1;i++)
                if(arr[i]>arr[i+1])
                    {
                        t = arr[i];
                        arr[i] = arr[i + 1];
                        arr[i + 1] = t;
                        flag=0;
                    }
            n--;
        } 
}
~~~