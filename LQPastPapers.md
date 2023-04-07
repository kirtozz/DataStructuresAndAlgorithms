## 蓝桥杯往年真题试做

* 快速空降目录         
    <a href='#B12th' >12th B.双阶乘</a>            
    <a href='#D12th' >12th D.整数分解</a>           
    <a href='#H12th' >12th H.完全平方数</a> 

---

<span id="B12th">12th B.双阶乘</span>    

>【问题描述】    
一个正整数的双阶乘，表示不超过这个正整数且与它有相同奇偶性的所有
正整数乘积。n 的双阶乘用 n!! 表示。    
例如：    
3!! = 3 × 1 = 3。    
8!! = 8 × 6 × 4 × 2 = 384。    
11!! = 11 × 9 × 7 × 5 × 3 × 1 = 10395。    
请问，2021!! 的最后 5 位（这里指十进制位）是多少？        
注意：2021!! = 2021 × 2019 × · · · × 5 × 3 × 1。           

~~~
#include<iostream>
using namespace std;
typedef long long ll;
int main(){
	ll ans=1;
	for(int i=1;i<=2021;i+=2){
		ans*=i;
		ans%=100000;    //(a * b) mod m = ((a mod m) * (b mod m)) mod m    
	}
	cout<<ans;
	return 0;
}    

关键在于取后五位的余数，因为C++不支持存储超过long long类型大小（64 bit）的数据。    
~~~

---

<span id="D12th">12th D.整数分解</span>        

>【问题描述】    
将 3 分解成两个正整数的和，有两种分解方法，分别是 3 = 1 + 2 和
3 = 2 + 1。注意顺序不同算不同的方法。        
将 5 分解成三个正整数的和，有 6 种分解方法，它们是 1+1+3=1+2+2=1+3+1=2+1+2=2+2+1=3+1+1。        
请问，将 2021 分解成五个正整数的和，有多少种分解方法？    

![LQ1.png](/pictures/LQ1.png "暴力失败,跑了几分钟毫无进展")            

~~~
看看大佬的解法：    
暴力+优化（三重循环）    
找规律：当我们确定了分解的前三位时，我们可以观察后面的两位是什么规律        
2017 1 1 1 1 （一种）        
2016 1 1 1 2          2016 1 1 2 1（两种）        
2015 1 1 1 3          2015 1 1 3 1          2015 1 1 2 2 （三种）        
我们可以观察到：后面两位的排列组合的最大值，是后面两位数和，再减1。    

#include <iostream>
using namespace std;

long long ans;
int main()
{
    for (int i = 1; i <= 2021; i++)
        for (int j = 1; j <= 2021; j++)
            for (int k = 1; k <= 2021; k++)
            {
                int tmp = 2021 - i - j - k;
                if (tmp >= 2)
                    ans += (tmp - 1);
            }
    cout << ans << endl;
    return 0;
}

不需要暴力，数列+组合数学    
我们可以把2021看成是2021个都是一的数列（1....1），两个一之间就存在一个间隔。我们就可以通过取间隔的方法将2021个1分成5段。        
如：将5分成三段        
1  ||||   1      1   ||||   1      1    
我们只需要再四个间隔里任意的取两个间隔就行了。    
通过推理，我们知道n个数就会有n-1个间隔，想分成n段就需要n-1个间隔。        
所以，我们只需要再2020个间隔里面任意的取4个间隔就能求出答案！组合数学C 2020_4就是答案！     

#include <iostream>
using namespace std;

// int main()
// {
//     long long ans = (2020 * 2019 * 2018 * 2017) / (4 * 3 * 2 * 1);
//     printf("%lld", ans);
//     return 0;
// }       // cout:8582718  乘的时候溢出了

int main()
{
    long long t = 2020 * 2019;
    t = t * 2018;
    t = t * 2017;
    t /= 24;
    printf("%lld", t);
    return 0; // cout:691677274345    正确答案    
}
~~~

---

<span id="H12th">12th H.完全平方数</span>        

>【问题描述】    
一个整数 a 是一个完全平方数，是指它是某一个整数的平方，即存在一个整数 b，使得 a = b^2^。    
给定一个正整数 n，请找到最小的正整数 x，使得它们的乘积是一个完全平方数。        
【输入格式】        
输入一行包含一个正整数 n。        
【输出格式】        
输出找到的最小的正整数 x。    
【样例输入 1】    
12    
【样例输出 1】    
3    
【样例输入 2】    
15    
【样例输出 2】    
15    
【评测用例规模与约定】
对于 30% 的评测用例，1 ≤ n ≤ 1000，答案不超过 1000。    

~~~
暴力超时    
#include <bits/stdc++.h>
using namespace std;

typedef long long LL;

bool is(LL x)
{
    return (LL)sqrt(x) * (LL)sqrt(x) == x; //强制类型转换LL
}

int main()
{
    LL n;
    cin >> n;

    for (LL i = 1; i <= n; i++)
        if (is(n * i))
        {
            cout << i << endl;
            break;
        }

    return 0;
}

优化解题思路：
任意一个正整数都可以被分解成若干个质数乘积的形式，例如40 =2^3 × 5^1;        
若一个数是完全平方数，那么其质因子的幂次必须都是偶数，例如400 = 2^4 × 5^2,因为20 = 2^2 × 5^1;    
因此若想将40改成完全平方数，只需要补上一个2和一个5，所以 X =2 × 5=10;        

#include <bits/stdc++.h>
using namespace std;

typedef long long LL;

int main()
{
    LL n;
    cin >> n;
    
    LL ans = 1;
    for (int i = 2; i <= n / i; i ++)
        if(n % i == 0)
        {
            int k = 0;
            while(n % i == 0) n /= i, k ++;
            if(k & 1) ans *= i;
        }
    
    if(n > 1) ans *= n;

    cout << ans << endl;        
    return 0;
}
~~~    


