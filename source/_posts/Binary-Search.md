---
title: Binary Search
author: Raptazure
categories: Algorithms

---



### 1.定义：

​	给定N个从小到大**排好序**的整数序列List[]，以及某待查找整数X，我们的目标是找到X在List中的下标。即若有List[i]=X，则返回i；否则返回-1表示没有找到。

<!-- more -->

​    二分法是先找到序列的中点List[M]，与X进行比较，若相等则返回中点下标；否则，若List[M]>X，则在左边的子系列中查找X；若List[M]<X，则在右边的子系列中查找X。

### 2.伪码描述：

```
{
     int left = 0;
     int right = n-1;
     while(left 小于等于 right)
     {
         int mid = (left + right) / 2;
         if(List[mid] == X)
             返回 mid;
         else if(List[mid] < X)
             left = mid+1;
         else if(List[mid] > X)
             right = mid-1;
     }
     return -1;
}
```

> 最坏情况下的时间复杂度：O(logn)，一直找不到，但是一直排除一半的值
>
> 最好情况下的时间复杂度：O(1)，第一个就找到了
>
> 空间复杂度：O(1)

### 3.算法实现：

```c

#include<iostream>
using namespace std;
int BinarySearch(int a[],int x,int n);
int main()
{
    int n,x,a[10000];
    cin>>n;
    cin>>x;
    for (int i = 0; i < n; i++)
    {
        cin>>a[i];
        //需要保证输入有序
    }
    int result = BinarySearch(a,x,n);
    cout<<result<<endl;
    return 0;
}
​
int BinarySearch(int a[],int x,int n)
{
    int left = 0;
    int right = n - 1;
    while (left<=right)
    {
        int mid = (left + right)/2;
        if(a[mid]==x)
            return mid;
        else if(a[mid]<x)
            left = mid+1;
        else if(a[mid]>x)
            right = mid-1;
    }
    return -1;
}

/*
输入样例
9
44
11 22 33 44 55 66 77 88 99
输出为所寻数的index，即要找的数为数组中从左往右数第inex+1个
*/
```

