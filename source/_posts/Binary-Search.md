---
title: Binary Search
author: Raptazure
categories: 编程
tags: 算法
date: 2019-10-27
---

## 1.二分模板

#### 整数二分：

```cpp
//mid属于左边：区间[1, r]被划分为[1, mid]和[mid+1, r]时使用
int bsearch_1(int l, int r)
{
    while (l < r)
    {
        int mid = (l + r) / 2;
        if(check(mid)) r = mid;
        //check()判断mid是否满足性质
        else l = mid + 1;
    }
    return 1;
}
//mid属于右边：区间[1, r]被划分为[1, mid - 1]和[mid, r]时使用
int bsearch_2(int l, int r)
{
    while (l < r)
    {
        int mid = (l + r + 1) / 2;
        if(check(mid)) l = mid;
        else r = mid - 1;
    }
    return 1;
}
```

<!-- more -->

#### 浮点数二分：

```cpp
//浮点数二分没有边界问题，相对容易解决
#include<iostream>
using namespace std;
int main()
{
    double x;
    cin >> x;

    double l = 0, r = x;
    /* 不用精度判断而是直接迭代100次
    for (int i = 0; i < 100; i++)
    {
        double mid = (r + l) / 2;
        if(mid * mid >= x) r = mid;
        else l = mid;
    }
    */
    while (r - l > 1e-8)
    {
        double mid = (r + l) / 2;
        if(mid * mid >= x) r = mid;
        else l = mid;
    }
    printf("%lf\n",l);
    return 0;
}
```

## 2.伪码描述

​ 给定 N 个从小到大**排好序**的整数序列 List[]，以及某待查找整数 X，我们的目标是找到 X 在 List 中的下标。即若有 List[i]=X，则返回 i；否则返回-1 表示没有找到。
​ 二分法是先找到序列的中点 List[M]，与 X 进行比较，若相等则返回中点下标；否则，若 List[M]>X，则在左边的子系列中查找 X；若 List[M]<X，则在右边的子系列中查找 X。

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

## 3.算法实现

#### 一个普普通通的二分：

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

#### 整数二分：AcWing 789

```cpp
#include<iostream>

using namespace std;

 const int N = 1e6 + 10;

 int n, m;
 int q[N];

 int main()
 {
     scanf("%d%d",&n,&m);
     for (int i = 0; i < n; ++i) scanf("%d", &q[i]);
     while (m--)
     {
        int x;
        scanf("%d",&x);
        int l = 0, r = n - 1;
        while (l < r)
        {
            int mid = l + r >> 1;
            if(q[mid] >= x) r = mid;
            else l = mid + 1;
        }
        if(q[l] != x) cout << "-1 -1" << endl;
        else
        {
            cout << l << " ";

            int l = 0, r = n - 1;
            while (l < r)
            {
                int mid = l + r + 1 >> 1;
                if(q[mid] <= x) l = mid;
                else r = mid - 1;
            }
            cout << l << endl;
        }
     }
    return 0;
 }
```

#### 浮点数二分：AcWing 790

```cpp
#include<iostream>
using namespace std;
int main()
{
    double n;
    int flag = 0;
    cin >> n;
    if(n <= 0)
    {
        flag = 1;
        n = -n;
    }
    double l = 0, r = n;
    for (int i = 0; i < 100; ++i)
    {
        double mid = (r + l) / 2;
        if(mid * mid * mid >= n)  r = mid;
        else l = mid;
    }
    if(flag) printf("-");
    printf("%.6lf",l);
    return 0;
}
```
