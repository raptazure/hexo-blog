---
title: PAT B
categories: Algorithms

---

# 字符串处理

## 1002 写出这个数

读入一个正整数 *n*，计算其各位数字之和，用汉语拼音写出和的每一位数字。

<!--more-->

### 输入格式：

每个测试输入包含 1 个测试用例，即给出自然数 *n* 的值。这里保证 *n* 小于 10100。

### 输出格式：

在一行内输出 *n* 的各位数字之和的每一位，拼音数字间有 1 空格，但一行中最后一个拼音数字后没有空格。

### 输入样例：

```in
1234567890987654321123456789
```

### 输出样例：

```out
yi san wu
```

### Solution：

​		因为要读入的数字太大，所以用字符串读入，在求和时就要考虑将字符串数字转换为整数，此后，为了方便获取和sum的位数，可以再使用`to_string`将sum转化为字符串num，之后利用`lenth()`函数得出元素个数，通过str数组与num数组的元素对应关系遍历输出结果。此外还要注意输出时最后一个拼音后面不要有空格。

```c++
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string s;
    cin >> s;
    int sum = 0;
    string str[10] = {"ling", "yi", "er", "san", "si", "wu", "liu", "qi", "ba", "jiu"};
    for(int i = 0; i < s.length(); i++)
        sum += (s[i] - '0');
    string num = to_string(sum);
    for(int i = 0; i < num.length(); i++)
    {
        if(i != 0) cout << " ";
        cout << str[num[i] - '0'];
    }
    return 0;
}
```
## 1003 我要通过！-  数学题

“**答案正确**”是自动判题系统给出的最令人欢喜的回复。本题属于 PAT 的“**答案正确**”大派送 —— 只要读入的字符串满足下列条件，系统就输出“**答案正确**”，否则输出“**答案错误**”。

得到“**答案正确**”的条件是：

1. 字符串中必须仅有 `P`、 `A`、 `T`这三种字符，不可以包含其它字符；
2. 任意形如 `xPATx` 的字符串都可以获得“**答案正确**”，其中 `x` 或者是空字符串，或者是仅由字母 `A` 组成的字符串；
3. 如果 `aPbTc` 是正确的，那么 `aPbATca` 也是正确的，其中 `a`、 `b`、 `c` 均或者是空字符串，或者是仅由字母 `A` 组成的字符串。

现在就请你为 PAT 写一个自动裁判程序，判定哪些字符串是可以获得“**答案正确**”的。

### 输入格式：

每个测试输入包含 1 个测试用例。第 1 行给出一个正整数 *n* (<10)，是需要检测的字符串个数。接下来每个字符串占一行，字符串长度不超过 100，且不包含空格。

### 输出格式：

每个字符串的检测结果占一行，如果该字符串可以获得“**答案正确**”，则输出 `YES`，否则输出 `NO`。

### 输入样例：

```in
8
PAT
PAAT
AAPATAA
AAPAATAAAA
xPATx
PT
Whatever
APAAATAA
```

### 输出样例：

```out
YES
YES
YES
YES
NO
NO
NO
NO
```

### Solution：

​		分析题目中可以通过的字符串：

|  xPATx  |              aPbTc  ->  aPbATca              |
| :-----: | :------------------------------------------: |
|  APATA  | APATA -> APAATAA -> APAAATAAA -> APAAAATAAAA |
| AAPATAA |    AAPATAA -> AAPAATAAAA -> AAPAAATAAAAAA    |

可以发现：字符串中必须只有P，A，T，且P和T中间至少有一个A。字符串中只能有一个P和一个T。中间和首尾可以插入A，但是需要满足开头A个数 × 中间A个数 = 末尾A个数。

```cpp
#include <iostream>
#include <map>
using namespace std;
int main()
{
    string s;
    int n, p = 0, t = 0;
    cin >> n;
    for(int i = 0; i < n; i++)
    {
        cin >> s;
        map<char, int> m;
        for(int j = 0; j < s.size(); j++)
        {
            m[s[j]]++;//统计P A T个数
            if(s[j] == 'P') p = j;//记录P的index
            if(s[j] == 'T') t = j;//记录T的index
        }
        //只有一个P，有A，只有一个T，仅有P A T三种字母，P和T之间要有字母，开头A个数 × 中间A个数 = 末尾A个数
        if(m['P'] == 1 && m['A'] != 0 && m['T'] == 1 && m.size() == 3 && t - p != 1 && p * (t - p -1) == s.size() - t - 1)
            printf("YES\n");
        else printf("NO\n");
	}
    return 0;
}
```

# 模拟：

## 1001 害死人不偿命的(3n+1)猜想 

卡拉兹(Callatz)猜想：

对任何一个正整数 *n*，如果它是偶数，那么把它砍掉一半；如果它是奇数，那么把 (3*n*+1) 砍掉一半。这样一直反复砍下去，最后一定在某一步得到 *n*=1。卡拉兹在 1950 年的世界数学家大会上公布了这个猜想，传说当时耶鲁大学师生齐动员，拼命想证明这个貌似很傻很天真的命题，结果闹得学生们无心学业，一心只证 (3*n*+1)，以至于有人说这是一个阴谋，卡拉兹是在蓄意延缓美国数学界教学与科研的进展……

<!-- more-->

我们今天的题目不是证明卡拉兹猜想，而是对给定的任一不超过 1000 的正整数 *n*，简单地数一下，需要多少步（砍几下）才能得到 *n*=1？

### 输入格式：

每个测试输入包含 1 个测试用例，即给出正整数 *n* 的值。

### 输出格式：

输出从 *n* 计算到 1 需要的步数。

### 输入样例：

```in
3
```

### 输出样例：

```out
5
```

### Solution：

​		第一题，没啥好说的//

```cpp
#include <iostream>
using namespace std;
int main()
{
    int n, cnt = 0;
    cin >> n;
    while(n != 1)
    {
        if(n % 2 == 0)
            n /= 2;
        else
            n = (3 * n + 1) / 2;
        cnt ++;
    }
    cout << cnt << endl;
    return 0;
}
```

