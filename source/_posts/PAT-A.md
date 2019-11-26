---
title: PAT A
categories: Algorithms
---
# Sort
## 1025 PAT Ranking

Programming Ability Test (PAT) is organized by the College of Computer Science and Technology of Zhejiang University. Each test is supposed to run simultaneously in several places, and the ranklists will be merged immediately after the test. Now it is your job to write a program to correctly merge all the ranklists and generate the final rank.

<!--more-->
### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive number *N* (≤100), the number of test locations. Then *N* ranklists follow, each starts with a line containing a positive integer *K* (≤300), the number of testees, and then *K* lines containing the registration number (a 13-digit number) and the total score of each testee. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, first print in one line the total number of testees. Then print the final ranklist in the following format:

```
registration_number final_rank location_number local_rank
```

The locations are numbered from 1 to *N*. The output must be sorted in nondecreasing order of the final ranks. The testees with the same score must have the same rank, and the output must be sorted in nondecreasing order of their registration numbers.

### Sample Input:

```in
2
5
1234567890001 95
1234567890005 100
1234567890003 95
1234567890002 77
1234567890004 85
4
1234567890013 65
1234567890011 25
1234567890014 100
1234567890012 85
```

### Sample Output:

```out
9
1234567890005 1 1 1
1234567890014 1 2 1
1234567890001 3 1 2
1234567890003 3 1 2
1234567890004 5 1 4
1234567890012 5 2 2
1234567890002 7 1 5
1234567890013 8 2 3
1234567890011 9 2 4
```

### Solution:

- [x]  01


- 在结构体中存放准考证号，分数，考场号以及考场内排名

- cmp: 分数从大到小，分数相同准考证号从小到大

- 步骤：

  - 按考场读入各考生信息，并对当前读入考场所有考生排序，之后将该考场所有考生排名写入结构体

  - 对所有考生排序

  - 按顺序一边计算总排名一边输出所有考生信息
  
- 注意：

  
  - 对同一考场考生单独排序：int num存放当前获取的考生数，每读入一个考生的信息就num++，这样读完一个考场的考生信息后，这个考场的考生对应的数组下标便为[num - k, num]。
  - 相同的分数情况下按照学号的从小到大排列，但是他们的排名应该是一样的数字。
  
  ```cpp
  #include <cstdio>
  #include <cstring>
  #include <algorithm>
  using namespace std;
  struct Student{
      char id[15];
      int score;
      int location_num;
      int local_rank;
  }stu[30010];
  bool cmp(Student a, Student b)
  {
      if(a.score != b.score) return a.score > b.score;
      else return strcmp(a.id, b.id) < 0;
  }
  int main()
  {
      //num - total testees, n - locations
      int n, k, num = 0;
      scanf("%d", &n);
      for(int i = 1; i <= n; i++)
      {
          //k - local testees
          scanf("%d", &k);
          for(int j = 0; j < k; j++)
          {
              scanf("%s %d", stu[num].id, &stu[num].score);
              //this testee's location number is i
              stu[num].location_num = i;
              //total_testees ++
              num++;
          }
          //sort testees of current location
          sort(stu + num - k, stu + num, cmp);
          //mark 1st of current location
          stu[num - k].local_rank = 1;
          //mark the others' rank
          for(int j = num - k + 1; j < num; j++)
          {
              if(stu[j].score == stu[j - 1].score)
                  stu[j].local_rank = stu[j - 1].local_rank;
              else stu[j].local_rank = j + 1 - (num - k);
          }
      }
      printf("%d\n", num);
      sort(stu, stu + num, cmp);
      int r = 1;
      for(int i = 0; i < num; i++)
      {
          if(i > 0 && stu[i].score != stu[i - 1].score)
              r = i + 1;
          printf("%s ",stu[i].id);
          printf("%d %d %d\n", r, stu[i].location_num, stu[i].local_rank);
      }
      return 0;
  }
  ```


- [x]  02


- 利用vector储存数据。先在考场内排名，将某地区排名完成的结构体local[j]赋给总体结构体数组total，然后进行总排名，最后输出。注意输入数据对准考证号位数的要求，不加013最后一个用例会挂掉…

  ```cpp
  #include <iostream>
  #include <algorithm>
  #include <vector>
  using namespace std;
  struct Stu{
      int local_rank, totoal_rank, score, location_num;
      long long int id;
  };
  bool cmp(Stu a, Stu b)
  {
      return a.score != b.score ? a.score > b.score : a.id < b.id;
  }
  int main()
  {
      int n, m;
      scanf("%d", &n);
      vector<Stu> total;
      for(int i = 1; i <= n; ++i)
      {
          scanf("%d", &m);
          vector<Stu> local(m);
          for(int j = 0; j < m; ++j)
          {
              scanf("%lld %d", &local[j].id, &local[j].score);
              local[j].location_num = i;
          }
          sort(local.begin(), local.end(), cmp);
          local[0].local_rank = 1;
          total.push_back(local[0]);
          for(int j = 1; j < m; j++)
          {
              local[j].local_rank = (local[j].score == local[j - 1].score) ? (local[j - 1].local_rank) : (j + 1);
              total.push_back(local[j]);
          }
      }
      sort(total.begin(), total.end(), cmp);
      total[0].totoal_rank = 1;
      for(int j = 1; j < total.size(); j++)
          total[j].totoal_rank = (total[j].score == total[j - 1].score) ? (total[j - 1].totoal_rank) : (j + 1);
      printf("%ld\n", total.size());
      for(int i = 0; i < total.size(); i++)
      // K lines containing the registration number (a 13-digit number)
          printf("%013lld %d %d %d\n", total[i].id, total[i].totoal_rank, total[i].location_num, total[i].local_rank);
      return 0;
  }
  ```


