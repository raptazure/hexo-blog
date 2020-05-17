---
date: 2019-11-05
title: Max Subsequnce Sum
categories: 编程
tags: 算法
mathjax: true
---
- 给定N个整数的序列*{A1,A2, ... ,An}*，求函数的最大值：

  $$\ f(x) = \max\{0,\sum\limits_{k=1}^{n}Ak \}$$
  
  <!-- more -->

1.最暴力：把所有连续子列和都算出来，从中找最大的那个。

```cpp
int MaxSubseqSum1 (int a[], int N) {
    int ThisSum,Maxsum=0;
    int i,j,k;
    //i为子列左端位置，j为子列右端位置，ThisSum为A[i]到A[j]子列和
    for ( i = 0; i < N; i++) {
        for ( j = i; j < N; j++) {
            ThisSum = 0;
            for ( k = 0; k <= j; k++)
                ThisSum += a[k];
            if (ThisSum > Maxsum)
                Maxsum = ThisSum;
        }
    }
    return Maxsum;
}
```

   时间复杂度为O(n^3^) ---三层循环嵌套  其实当知道从i到j和的时候，要加上下一个j时没有必要从头往后加，可加一个元素。

2.省略k循环：

```cpp
int MaxSubseqSum2 (int a[], int N) {
    int ThisSum, Maxsum = 0;
    int i, j;
    for ( i = 0; i < N; i++) {
        ThisSum = 0;
        for ( j = i; j < N; j++) {
            //对于相同的i，不同的j，在j-1次循环基础累加1即可
            ThisSum += a[j];
            if (ThisSum > Maxsum)
               Maxsum = ThisSum;
        }
    }
    return Maxsum;
}
```

​      时间复杂度为O(n2）--->  可否改进为O(nlogn)

3.分治算法：

​	 把一个复杂的问题切分成很多小块，然后分头解决他们，最后合并结果。把数组从中间一分为二，递归地解决左右两边的问题。但还要考虑跨越边界的子列和。

```cpp
//递归分成两份，分别求每个分割后最大子列和，时间复杂度为 O(n*logn)
/* 返回三者中最大值*/
int Max3(int A,int B,int C){
    return (A>B)?((A>C)?A:C):((B>C)?B:C);
}
int DivideAndConquer(int a[],int left,int right){
    
    /*递归结束条件：子列只有一个数字*/
    // 当该数为正数时，最大子列和为其本身
    // 当该数为负数时，最大子列和为 0
    if(left == right){
        if(0 < a[left])  
            return a[left];
        return 0;
    }
    
    /* 分别递归找到左右最大子列和*/ 
    int center = (left+right)/2; 
    int MaxLeftSum = DivideAndConquer(a,left,center);
    int MaxRightSum = DivideAndConquer(a,center+1,right);
    
    /* 再分别找左右跨界最大子列和*/
    int MaxLeftBorderSum = 0;
    int LeftBorderSum = 0;
    for(int i=center;i>=left;i--){  //应该从边界出发向左边找
        LeftBorderSum += a[i];
        if(MaxLeftBorderSum < LeftBorderSum)
 			MaxLeftBorderSum = LeftBorderSum;   
    }
    int MaXRightBorderSum = 0;
    int RightBorderSum = 0;
    for(int i=center+1;i<=right;i++){  // 从边界出发向右边找
        RightBorderSum += a[i];
        if(MaXRightBorderSum < RightBorderSum)
            MaXRightBorderSum = RightBorderSum;
    }
    
    /*最后返回分解的左边最大子列和，右边最大子列和，和跨界最大子列和三者中最大的数*/
	return Max3(MaxLeftSum,MaxRightSum,MaXRightBorderSum+MaxLeftBorderSum);
}
int MaxSubseqSum3(int n,int a[]){
    return DivideAndConquer(a,0,n-1);
}
```

4.在线处理（贪心算法）：

​      不从整体最优上考虑而是求出局部最优解，只关心子列和当前的大小，如果临时和加上一个负数，则置临时和为0。时间复杂度为O(n)。

```cpp
int MaxSubseqSum4(int n,int a[])
{
    int max = 0;
    int tmpSum = 0;
    for (int i = 0;i<n;i++)
    {
        tmpSum+=a[i];
        if(tmpSum<0)
            tmpSum = 0;
        else if (max<tmpSum)
            max=tmpSum;            
    }
    return max;
}
```
