
# note

## PAT

### [1001 A+B Format](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)[(20分)](https://github.com/Mifan-rabbit/PTA/blob/master/1001%20A%2BB%20Format%20(20%E5%88%86).md)

- 六位数相加减，结果是可以枚举的，共三种：①A; ②A,B; ③A,B,C;
- 直接输出时，若结果为1000，则输出为1,0，故需要格式化输出
- 一开始的解题思路是使用vector，每模1000，就压入vector，但欠考虑和为0时，vector为空

### [1002 A+B for Polynomials (25分](https://pintia.cn/problem-sets/994805342720868352/problems/994805526272000000)

- 声明变量时注意变量类型，exponents(指数)为整数，coefficients(系数)为浮点数
- 循环注意次数及范围
  - K  N1  aN1  N2  aN2  ...  Nk  aNk
  - 1 ≤ K ≤ 10 => 最多有十个数系数不为零
  - 0 ≤ Nk ≤ ... ≤ N2 ≤ N1 ≤ 1000 =>指数的范围

### [1010 Radix (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805507225665536)

- 该题用二分法求对应的进制
- 最大的数位为ans，进制数的底线是ans+1
- long long int 的最大值是 (1LL<<63)-1;

### [1016  Phone Bills  (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805493648703488)

- 配对必须保证 on-line 和 off-line 是时间上相邻的两条记录
- 题目要保证整个输入至少有一对有效通话记录，但不保证每个用户都有有效通话记录，因此一些不存在有效通话记录的用户不被输出
- 时长计算，对已知起始时间和终止时间，只需要不断将起始时间加1，判断其是否到达终止时间即可，代码如下：

  ```cpp
  while (start.day < end.day || start.hour < end.hour || start.minute < end.minute)
  {
    time++;      //该次记录总时间加1min
    start.minute++;     //当前时间加1min
    if (start.minute == 60)  //当前分钟数到达60
    {
      start.minute = 0;   //进入下一个小时
      start.hour++;
    }
    if (start.hour == 24)   //当前小时数到达24
    {
      start.hour = 0;   //进入下一天
      start.day++;
    }
  }
  ```

### [1025 PAT Ranking (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805474338127872)

- sort函数
  - 头文件 algorithm
  - 方式 sort(首元素地址, 尾元素地址的下一个地址, 比较函数(非必填))
  
- strcmp函数
  - 头文件 string.h 或者 cstring
  - 方式 strcmp(str1, str2)
    - 若str1=str2，则返回零
    - 当str1的字典顺序小于str2时返回一个负数，注意，这个负数不一定是-1，具体和编译器相关

- 实现排名
  - 分数不同排名不同，分数相同排名相同，且占用一个排位。所以91、90、88、88、84的排名应该算1、2、3、3、5。具体实现时，切忌算作1、2、3、3、4。

  - ``` cpp
     stu[0]=1;
     for(int i=1; i<num; ++i)
     {
      if(stu[i].score == stu[i-1].score)
        stu[i].rank = stu[i-1].rank;
      else
        stu[i].rank = i+1;
     }
    ```

### [1033  To Fill or Not to Fill  (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805458722734080)

- 购油策略，距离a<b<c时
  - 若油价a<b<c，则在a加油站加满油，再到b加油站考虑后续加油情况（没有更低油价的加油站时，前往油价尽可能低的加油站）
    - 若油价a>b>c，则在a加油站加油使储油量刚好到b加油站（优先前往更低油价的加油站）
    - 若满油情况下找不到加油站，则最远能到达的距离为当前加油站的距离上加满状态下能前进的距离
- 解题策略
  - 因为开始时，油箱为空，若与最近的加油站的距离不为0，汽车无法出发
  - 在终点设置一个油价为0的加油站，防止溢出

### [1035 Password (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805454989803520)

注意英文输出时单复数情况，当没有密码需要改时，输出==There are N accounts and no account is modified==，当N等于1时，输出==There is 1 account and no account is modified==

### [1038  Recover the Smallest Number  (30分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805449625288704)

- 32 321 3214 组成 321-3214-32 时数值最小，则要求每两个字符串满足 s1+s2<s2+s1(字符拼接)
- 还要注意前导零要除去，若去除前导零后串长变为0，则要输出“0”

### [1041  Be Unique  (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805444361437184)

- 题目要求在数列中找到最先出现的独一无二的数字
- 错误行为是从数列尾部开始遍历，一旦为第一次出现，当作当前的最先出现独一无二的数字。
- 正确做法应该是先计算数字出现次数，再从头开始遍历，寻找出现次数为1的数字

### [1065 A+B and C (64bit) (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805406352654336)

- 使用scanf输入长整型
- A, B的范围是 [-2^63^, 2^63^-1]
  - 负溢出 A+B≥0
  - 正溢出 A+B<0

### [1073 Scientific Notation (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805395707510784)

该题目是要将科学计数形式(*[+-][1-9].[0-9]+E[+-][0-9]+*) 转化为小数，根据指数的零正负分为三类讨论：

- 指数为**零**，直接输出结果
- 指数为**正**,小数点右移
  - $P['E']-P['.']≥n_{指数}$ 时,无需补零,但要注意等号刚好成立时无需在末尾加小数点
  - 否则需要补 $n_{指数}-P['E']-P['.']$ 个**零**
- 指数为**负**,小数点左移,补 $n_{指数}-1$ 个**零**

### [1075  PAT Judge  (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805393241260032)

- 输出规则中隐含了一个边界情况：某考生的所有能通过编译的提交都获得了0分，这时考生的总分是0分，但是这条信息仍然要被输出

### [1077 Kuchiguse (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805390896644096)

- cin 不能读取换行符和空格
- getchar() 接收多余的换行符
- getline(cin, s) s为string对象，按行读取句子

### [1078  Hashing  (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805389634158592)

- Quadratic problem 是指二次探测方法，即当H(a)发生冲突时，让a按a+1^2^，a-1^2^，a+2^2^，a-2^2^……，a+（Tsize-1）^2^，a-（Tsize-1)^2^的顺序调整a的值。本题目说明只要往正向解决冲突，因此需要按a+1^2^，a+2^2^，a+3^2^，a+4^2^……的顺序调整a的值。

### [1088  Rational Arithmetic  (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805378443755520)

- 简化分数的时候，有可能分子分母用辗转相除法返回的公因数为0，缺少对公因数的判断，会导致异常

### [1089  Insert or Merge  (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805377432928256)

- 根据初始数列和目标数列，问它是由插入排序还是归并排序产生的，并输出下一步将产生的序列
- 一开始是寻找最长递增序列，通过一次比较看出是不是归并排序，但这个不合理，应该模拟归并排序，比较过程中数列是否相同来确定
- 这里数据范围很小，归并函数中可以不写合并函数，而直接用sort代替
- 陷阱，可能初始数列和目标数列相同，可能产生双解

### [1095  Cars on Campus  (30分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805371602845696)

- 删除数组中无效数据时，用两个指针分别指向当前遍历的元素和有效元素的下一位，由于该题同时移动n和n+1个元素，注意访问的第n个元素可能被其它元素覆盖
- 使用map记录车牌号对应的停车时长 -------------------- ```map<string, int> parking;```
  - 第一次使用时初始化 -------------------- ```if (parking.count(id) == 0)     parking[id] = 0;```
    - 遍历时 --------------------  ```for (auto  it = parking.begin(); it  !=  parking.end(); ++it)
 {if (it->second == maxtime)    printf("%s ", it->first.c_str());}```

### [1096  Consecutive Factors  (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805370650738688)

- 本题是求最长的起始数字最小的因子序列

  ```cpp
  for (long  long  int  i = 2; i <= (long  long  int)sqrt(1.0 * n); ++i) //遍历连续发第一个整数
  {
    long  long  temp = 1, j = i; //temp为当前连续整数的乘积
    while (true) //让j不断加1，看看最长能到多少
    {
      temp *= j; //当前连续整数的乘积
      if (N % temp != 0) //如果不能被n整除，就结束计算
        break;
      if (j - i + 1 > len) //发现了更长的长度
      {
        ansi = i; //更新第一个整数
        ansj = j;
        len = j - i + 1; //跟新最长长度
      }
      j++; //下一个整数
    }
  }
  ```

### [1104  Sum of Number Segments  (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805363914686464)

- 这是一道通过找规律解决的题目
- double型在运算过程中，可能无法精确地表示数据造成误差，可以用long double

## LeetCode

### [1163. Last Substring in Lexicographical OrderHard](https://leetcode.com/problems/last-substring-in-lexicographical-order/)

- C++ String的使用

截取子串
  
| 函数             |                                                           |
|:-----------------|:----------------------------------------------------------|
| s.substr(pos, n) | 截取s中从pos开始（包括0）的n个字符的子串，并返回          |
| s.substr(pos)    | 截取s中从从pos开始（包括0）到末尾的所有字符的子串，并返回 |
  
替换子串
  
| 函数                   |                                              |
|:-----------------------|:---------------------------------------------|
| s.replace(pos, n, s1)) | 用s1替换s中从pos开始（包括0）的n个字符的子串 |
  
查找子串

| 函数                   |                                                                |
|:-----------------------|:---------------------------------------------------------------|
| s.find(s1)             | 查找s中第一次出现s1的位置，并返回（包括0）                     |
| s.rfind(s1)            | 查找s中最后次出现s1的位置，并返回（包括0）                     |
| s.find_first_of(s1)    | 查找在s1中任意一个字符在s中第一次出现的位置，并返回（包括0）   |
| s.find_last_of(s1)     | 查找在s1中任意一个字符在s中最后一次出现的位置，并返回（包括0） |
| s.fin_first_not_of(s1) | 查找s中第一个不属于s1中的字符的位置，并返回（包括0）           |
| s.fin_last_not_of(s1)  | 查找s中最后一个不属于s1中的字符的位置，并返回（包括0）         |
  
- 解题边界问题
    1. 按字典顺序，可以通过比较字符的大小得出，但在当输入为 4\*10^5 个相同字符时，会有可能超时
    2. 我的想法是，按字符串顺序搜索字典序列最大的字母，若遇到大小相同的字符，就依次比较其后跟字符大小，这时会有三种情况：
        1. 出现比子串开头更大的字母，则改变子串开头字符，从这个字符开始继续搜索
        2. 后跟字符不相等，选择后跟字符大的，继续搜索
        3. 其中一个遍历到字符串末尾，则最大子串已经找到

## 书

### 字符串hash（散列）

**将一个二维整点P的坐标映射为一个整数，使整点P可以由该整数唯一地代表**  
可以假设一个整数P的坐标 （x，y），其中 0≤x,y≤Range，**那么可以令hash函数为:**$$ H(P) = x * Range + y $$  

**字符串hash是指一个字符串S映射为一个整数**，先假设字符串均由大写字母A~Z构成。

``` cpp
int hashFunc(char s[], int len){
int id = 0;
for(int i = 0; i < len; i++)
    id = id*26 + ( s[i] - 'A')
return id;
}
```

### 全排列（递归）

一般把 1\~n 这n个整数按某个顺序摆放的结果称为这n个整数的**一个排列**，而全排列指这n个整数能形成的所有排列。现在需要**按字典序**从小到大的顺序输出 1\~n 的全排列。  

``` cpp
void generateP(int index)
{
    if(index==n+1)               //递归边界
    {
        for(int i=1; i<=n; i++)P
            cout<<P[i]<<" ";    //输出当前列表
        return ;
    }

    for(int x=1; x<=n; x++)
    {
        if(hashTable[x]==false) //x没有在排列当中
        {P
            P[index]=x;
            hashTable[x]=true;  //表示x已在排列当中
            generateP(index+1); //处理下一个位置
            hashTable[x]=false; //还原
        }
    }
}
```

### n皇后

要求n个皇后两两不在同一行、同一列、同一条对角线上，求方案

1. 递归
    运用**全排序**，获得每一列的皇后所在行号，在递归边界时进行合理性判断  
2. 回溯   <small>(在到达递归边界前的某层，由于一些事实导致已经不需要往任何一个子问题递归，就可以直接返回上一层)</small>
    确定第n个皇后的位置时，保证其不与前n-1个皇后冲突

### 二分

1. 当 $mid=(left+right)/2$ 中的 $left+right$ 可能超过 int 而导致溢出，此时可以改用 $mid=left+(right-left)/2$  

2. 如果递增序列A中的元素可能重复，那么如何对给定的欲查询元素x，求出序列中第一个大于等于x的元素的位置L以及第一个大于x的元素的位置R，这样元素x在序列中的存在区间就是[L,R)。  
二分下界是0是显然的，但二分上界是n-1还是n呢？考虑到查询元素有可能比序列中的所有元素都要大，此时应当返回n  

3. ```cpp
   int solve(int left, int right){
     int mid;
     while(left<right){       //若区间为左开右闭，则循环条件为left+1<right
       mid = (left+right)/2;
       if(条件成立)
         right=mid;
       else
         left=mid+1;
     }
     return left;
   }
   ```

4. **木棒切割问题**：给出N根木棒，长度均已知，现希望通过切割它们来得到至少K段长度相等的木棒（长度必须是整数），问这些长度相等的木棒最长能有多长。

> - 根据对当前长度L来说能得到的木棒段数k与K的大小来进行二分，寻找最后一个满足k≥K的长度L。  

5. **多边形组成的凸边形的外接圆的最大半径**：给出N个线段长度，试将它们头尾相接组合成一个凸多边形，使凸多边形的外接圆（多边形每个顶点都在圆上）的半径最大，求该最大半径。其中$N<=10^5$，线段长度均不超过100，要求算法中不涉及坐标的计算。

> - 最大半径一定大于等于最长边的一半
> - 若圆心在多边形内部，则所有边对应的圆心角之和为2π
>   - 圆心角之和sum<2?π，线段没法首尾相连的在外接圆上，半径变小
>   - 圆心角之和sum>2?π，半应变大
> - 若圆心在多边形外部，则最长边对应的圆心角为其它边对应的圆心角之和
>   - 如果除去最大圆心角的其他圆心角之和小于π，说明圆心在多边形外面
>   - 当最大圆心角小于其它角时，半径变大
>   - 当最大圆心角大于其它角时，半径变小

### 最大公约数与最小公倍数

1. 最大公约数

> 设a、b均为正整数，则gcd(a,b)=gcd(b,a%b)。  
> **证明**：设$a=kb+r$，则有$r=a-kb$
> 设d为a、b的一个公约数，那么d也是r的一个约数，则d是b、r的一个公约数。
>
> ```cpp
> int gcd(int a, int b)
> {
>     return !b ? a : gcd(b, a%b); //a<b则ab交换
> }```

2.最小公倍数
>$lcm(a,b)=\frac {ab}{gcd(a,b)}$
>ab在实际计算时可能溢出，更恰当的写法是 $lcm(a,b)=\frac {a}{gcd(a,b)}*b$

### 素数

1. 素数的判断

  ```cpp
  #include <math.h>
  bool isPrime(int n)
  {
      if (n <= 1)
          return false;
      int sqr = (int)sqrt(1.0 * n);
      for (int i = 2; i <= sqr; i++) //遍历2~根号n
          if (n % i == 0)
              return false;
      return true;
  }
  ```
