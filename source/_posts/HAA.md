---
title: 高精度加法模板及应用
categories: Algorithms
tags: LeetCode
---

### 引入

- 高精度加法通过对数位分别储存运算，并维护一个用于处理进位的变量，从而在不造成溢出的前提下实现大数相加。
- Java和Python中虽然不需要考虑大整数相加的溢出问题，但这种算法的思想很值得借鉴。
- 这种思想在很多问题上都可以应用，这里选取LC的几道题目进行分析

<!--more-->

### 模板

```cpp
#include<iostream>
#include<vector>

using namespace std;
// 加引用避免再拷贝整个数组
vector<int> add(vector<int> &A, vector<int> &B) 
{
    // 定义储存结果的vector以及进位t，第0位没有进位->初始化为0
    vector<int> C;
    int t = 0;
    // 从个位开始遍历直至遍历完A和B的所有位
    for (int i = 0; i < A.size() || i < B.size(); i++)
    {
        // 每一次用t表示Ai，Bi与上一个数的进位这三个数的和
        if(i < A.size()) t += A[i];
        if(i < B.size()) t += B[i];
        // 当前这一位输出t除以10的余数
        C.push_back(t % 10);
        // t是否进位
        t /= 10;
    }
    // 如果最高位有进位则补1
    if(t) C.push_back(1);
    return C;
}
int main()
{
    // 使用字符串读入
    string a, b;
    vector<int> A, B;
    cin >> a >> b; //a = "123456"
    // 使用vector逆序读入,变成整数需要减去偏移量0
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');//A = [6,5,4,3,2,1]
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    // 相当于vector<int>
    auto C = add(A, B);
    // 倒序输出
    for (int i = C.size() - 1; i >= 0; i--) printf("%d", C[i]);
    return 0;
}

// 个位放在索引0的位置：出现进位的情况时需要在高位补上1,这样在数组后端补数比较容易
```
### 应用：
##### LC066 [Plus One](https://leetcode.com/problems/plus-one/)
- 实际就是只考虑+1特殊情况的简化版
- 逆序遍历`digits`数组，每次循环将`digits`的元素加到`t`上
- 仅当第一次遍历（个位）时使`t`额外加1
- 将当前位结果`t%10`存到答案`res`里
- 用`t/10`表示进位并进入下一次循环
- 遍历后，如果最高位仍有进位则补1
- 翻转数组得到答案
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> res;
        int t = 0;
        for(int i = digits.size() - 1; i >= 0; i--) {
            t += digits[i];
            if(i == digits.size() - 1) t += 1;
            res.push_back(t % 10);
            t /= 10;
        }
        if(t) res.push_back(1);
        reverse(res.begin(), res.end());
        return res;
    }
};
```
##### LC002 [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
- 这里其实就是采用链表储存数位，和使用数组一样，要注意访问元素的顺序。
- 注意到题中描述`The digits are stored in reverse order`，因此对于用例`[2->4->3] + [5->6->4]`，实际就是竖式计算`342+465`,这里个位已经位于等价于索引0的位置。
- 除了大数模板的应用外，还要注意一些链表中的常用技巧，比如可以设置`dummy`虚拟头节点用于新链表的构建。
```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto dummy = new ListNode(-1);
        ListNode* pre = dummy;
        int t = 0;
        while(l1 || l2 || t) {
            if(l1) {
                t += l1->val;
                l1 = l1->next;
            }
            if(l2) {
                t += l2->val;
                l2 = l2->next;
            }
            pre->next = new ListNode(t % 10);
            pre = pre->next;
            t /= 10;
        }
        return dummy->next;
    }
};
```
##### LC445 [Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)
- 注意题目描述`The most significant digit comes first`
- 如果不考虑`Follow up`，这道题链表反转后就和上面那道思路差不多了
- 链表反转可以通过迭代或者递归两种方法实现，这里采用双指针的迭代写法
- 完成加法后链表相对最后结果还是逆序的，需要再次反转
```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto head1 = reverse(l1);
        auto head2 = reverse(l2);
        auto dummy = new ListNode(-1);
        auto p = dummy;
        int t = 0;
        while(head1 || head2 || t) {
            if(head1) {
                t += head1->val;
                head1 = head1->next;
            }
            if(head2) {
                t += head2->val;
                head2 = head2->next;
            }
            p->next = new ListNode(t % 10);
            p = p->next;
            t /= 10;
        }
        return reverse(dummy->next);
    }
    ListNode* reverse(ListNode* head)
    {
        auto cur = head;
        ListNode* prev = nullptr;
        while(cur) {
            auto next = cur->next;
            cur->next = prev;
            prev = cur;
            cur = next;
        }
        return prev;
    }
};
```
##### LC067 [Add Binary](https://leetcode.com/problems/add-binary/comments/)
- 二进制加法和十进制方法差不多，只是处理进位时改为`t % 2 和 t /= 2`
- 通过`s[i] - '0'`将字符串中的字符依次转换为整形储存到动态数组里
- 类似于模板中的倒序输出，加法完成后需要反转答案数组`res`
- 使用`i + '0'`将答案数组转为字符串并返回该字符串
```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        string ans;
        vector<int> A, B;
        for(int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
        for(int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
        vector<int> res;
        int t = 0;
        for(int i = 0; i < A.size() || i < B.size(); i++) {
            if(i < A.size()) t += A[i];
            if(i < B.size()) t += B[i];
            res.push_back(t % 2);
            t /= 2;
        }
        if(t) res.push_back(1);
        reverse(res.begin(), res.end());
        for(int& i:res) ans.push_back(i + '0');
        return ans;
    }
};
```

