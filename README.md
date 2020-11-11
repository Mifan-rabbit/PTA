
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

### [1039 Course List for Student (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805447855292416)

- 题目是读取每门课的所有选课学生，然后将该课程编号加入所有选择该门课的学生中去。
- 本来想用map实现学生姓名和学生编号之间的映射，但会超时
- 用[字符串hash](#hash)进行求解

### [1041  Be Unique  (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805444361437184)

- 题目要求在数列中找到最先出现的独一无二的数字
- 错误行为是从数列尾部开始遍历，一旦为第一次出现，当作当前的最先出现独一无二的数字。
- 正确做法应该是先计算数字出现次数，再从头开始遍历，寻找出现次数为1的数字

### [1060 Are They Equal (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805413520719872)

- $0.a_1a_2...a_ka_{k+1}$ k是第一个非零位的下标
- $b_1b_2...b_n.a_1a_2...$

```cpp
int n; //有效位数
string deal(string s, int &e)
{
    int k = 0; //s的下标
    while (s.length() > 0 && s[0] == '0')
        s.erase(s.begin()); //去掉s的前导零
    if (s[0] == '.')        //若去掉前导零后是小数点，说明s是小于1的小数
    {
        s.erase(s.begin()); //去掉小数点
        while (s.length() > 0 && s[0] == '0')
        {
            e--;                //每去掉一个0，指数e减1
            s.erase(s.begin()); //去掉小数点后非零位前的所有零
        }
    }
    else
    {
        while (k < s.length() && s[k] != '.') //寻找小数点
        {
            k++;
            e++; //只要不遇到小数点，就让指数e++
        }
        if (k < s.length())
            s.erase(s.begin() + k);
    }
    if (s.length() == 0)
        e = 0; //如果去除前导零后长度为0，则说明这个数是0
    int num = 0;
    k = 0;
    string res;
    while (num < n) //只要精度还没有到n
    {
        if (k < s.length()) //只要还有数字，就加到res末尾
            res += s[k++];
        else
            res += '0'; //否则res末尾添加0
        num++;
    }
    return res;
}
```

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

### [1100 Mars Numbers (20分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805367156883456)

- 整行读取getline(cin, str);
- cin 不读取换行符，可用scanf("%d%*c", &n);

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

### 字符串hash（散列）<span id=hash>

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

### 数学问题

#### 最大公约数与最小公倍数

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

#### 素数

##### 1. 素数的判断

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

##### 2. 质因子分解

- 因为1本身不是素数，因此它没有质因子，题目中要对1进行处理  
- 考虑到 $2*3*5*7*11*13*17*19*23*29$ 已经超过int范围了，所以数组只需要开到10
- 对一个正整数n来说，如果它存在1和本身之外的因子，那么一定是在sqrt(n)的左右成对出现的，用在“质因子”上，对于正整数n，如果它存在[2,n]范围内的质因子，要么这些质因子全部小于等于sqrt(n)，要么只存在一个大于sqrt(n)的质因子
- 如果要求一个正整数N的因子个数，只需要对其质因子分解，得到各质因子 $p_i$ 的个数分别为 $c_1,c_2,……,c_k$，于是N的因子个数是$(c_1+1)*(c_2+1)*……*(c_k+1)$
- 同理，N的所有因子之和$(1+p_1+p_1^2+……+p_1^{c_1})*(1+p_2+p_2^2+……+p_2^{c_2})*……*(1+p_k+p_k^2+……+p_k^{c_k})=\frac{1-p_1^{c1+1}}{1-p_1}*\frac{1-p_2^{c2+1}}{1-p_2}*...\frac{1-p_k^{ck+1}}{1-p_k}$

##### 3. 大整数

###### 3.1 大整数的存储

```cpp
struct bign
{
    int d[1000];
    int len;
    bign()
    {
        memset(d, 0, sizeof(d));
        len = 0;
    }
};
```

###### 3.2 四则运算

- 高精度加法(都为正数)

    ```cpp
    bign add(bign a, bign b)
    {
        bign c;
        int carry = 0;                               //carry是进位
        for (int i = 0; i < a.len || i < b.len; i++) //以较长的为界限
        {
            int temp = a.d[i] + b.d[i] + carry;
            c.d[c.len++] = temp % 10;
            carry = temp / 10;
        }
        if (carry != 0) //如果最后进位不为0，则直接赋给结果的最高位
        {
            c.d[c.len++] = carry;
        }
        return c;
    }
      ```

- 高精度减法

    ```cpp
    bign sub(bign a, bign b)
    {
        bign c;
        for (int i = 0; i < a.len || i < b.len; i++)
        {
            if (a.d[i] < b.d[i]) //如果不够减
            {
                a.d[i + 1]--; //向高位借位
                a.d[i] += 10; //当前位加10
            }
            c.d[c.len++] = a.d[i] - b.d[i];
        }
        while (c.len -1 >= 1 && c.d[c.len - 1] == 0)
            c.len--; //去除最高位的0，同时至少保留一位最低为
        return c;
    }
    ```

- 高精度与低精度的乘法

    ```cpp
    bign multi(bign a, int b)
    {
        bign c;
        int carry = 0; //进位
        for (int i = 0; i < a.len; i++)
        {
            int temp = a.d[i] * b + carry;
            c.d[c.len++] = temp % 10;
            carry = temp / 10;
        }
        while (carry != 10) //和加法不一样，乘法的进位可能不止一位
        {
            c.d[c.len++] = carry % 10;
            carry /= 10;
        }
    }
    ```

- 高精度与低精度的除法

    ```cpp
    bign divide(bign a, int b, int &r) //r为余数
    {
        bign c;
        c.len = a.len;
        for (int i = a.len - 1; i >= 0; i--)
        {
            r = r * 10 + a.d[i];
            if (r < b)
                c.d[i] = 0;
            else
            {
                c.d[i] = r / b;
                r = r % b;
            }
        }
        while (c.len - 1 >= 1 && c.d[c.len - 1] == 0)
            c.len--;
        return c;
    }
    ```

##### 4. 欧几里得算法

###### 4.1 扩展欧几里得算法

> $$\begin{cases}
> ax_1 + by_1 = gcd(a, b)\\
> bx_2 + (a \pmod b) y_2 = gcd(b, a \pmod b)
> \end{cases}$$
> **得到递推公式：**
> $$\begin{cases}
> x_1 = y_1\\
> y_1 = x_2 - (a/b)y_2
> \end{cases}$$
> **通过一组解得到全部解** *(k为任意整数)* **：**
> $$\begin{cases}
> x' = x + \frac {b}{gcd} *k \\
> y' = y - \frac {a}{gcd} * k
> \end{cases}$$
> **可以得出最小的一组解：**
> $$\begin{cases}
> x_{min} = (x \pmod \frac {b}{gcd} + \frac {b}{gcd}) \pmod \frac {b}{gcd}\\
> y_{min} = (y \pmod \frac {a}{gcd} + \frac {a}{gcd}) \pmod \frac {a}{gcd}
> \end{cases}$$

```cpp
int exGcd(int a, int b, int &x, int &y)
{
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }
    int g = exGcd(b, a % b, x, y);
    int temp = x;
    x = y;
    y = temp - a / b * y;
    return g;
}
```

###### 4.2 方程 $ax+by=c$ 的求解

> $a x_0 + b y_0 = gcd$
> $a \frac {cx_0}{gcd} + b \frac {cy_0}{gcd} = c$
> 故当 $0 \equiv c \pmod {gcd} $ 时,一组解$(\frac {cx_0}{gcd}, \frac {cy_0}{gcd})$

###### 4.3 同余式 $ax \equiv c \pmod m$

> $0 \equiv (ax-c) \pmod m$
> 推出 $ ax - c = my$
> 令 y=-y,则
> $ax + my = c$

###### 4.4 逆元求解以及 $ (b/a) \pmod m$

> **解决** $(b/a)\%m \ne [(b\%m)/(a\%m)]%\m$
> 假设a、m是整数，求a模m的逆元,即 $ab \equiv 1 \pmod m$

```cpp
int inverse(int a, int m)
{
    int x, y;
    int g = exGcd(a, m, x, y); //求解 ax+my=1
    return (x % m + m) % m;    //a模m的逆元为最小正整数解 (x%m+m)%m
}
```

##### 5. 组合数

###### 5.1 $n!$中有$(\frac {n}{p}  + \frac {n}{p^2} + \frac {n}{p^3} + ...)$个质因子p

```cpp
//计算n!中有多少个质因子p
int cal(int n, int p)
{
    int ans = 0;
    while (n)
    {
        ans += n / p;
        n /= p; //相当于分母多乘一个p
    }
    return ans;
}

int cal(int n, int p)
{
    if (n < p)
        return 0;
    return n / p + cal(n / p, p);
}
```

通过这个算法，可以很快地计算出n!的末尾有多少个零

###### 5.2 计算 $C_n^m$

$C_n^m=C_{n-1}^m+C_{n-1}^{m-1}$

```cpp
// 递归求解
int res[100][100] = {0};
int C(int n, int m)
{
    if (m == 0 || m == n)
        return 1;
    if (res[n][m] != 0)
        return res[n][m];
    return res[n][m] = C(n - 1, m) + C(n - 1, m - 1);
}

//递推求解
int res[67][67] = {0};
const int n = 60;
void calC()
{
    for (int i = 0; i <= n; i++)
        res[i][0] = res[i][i] = 1;
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= i/2; j++)
        {
            res[i][j] = res[i - 1][j] + res[i - 1][j - 1];
            res[i][i - j] = res[i][j];
        }
    }
}
```

$C_n^m=\frac{n!}{m!(n-m)!}=\frac{(n-m+1)*(n-m+2)*...*(n-m+m)}{m*(m-1)*...*1}$

```cpp
// 定义式的变形计算
long long C(long long n, long long m)
{
    long long ans = 1;
    for (long long i = 1; i <= m; i++)
        ans = ans * (n - m + i) / i; //容易溢出
}
```

###### 5.3 计算 $C_n^m \pmod p$

- 方法一

```cpp
// 递归求解
int res[100][100] = {0};
int C(int n, int m, int p)
{
    if (m == 0 || m == n)
        return 1;
    if (res[n][m] != 0)
        return res[n][m];
    return res[n][m] = C(n - 1, m) + C(n - 1, m - 1) % p;
}

//递推求解
int res[67][67] = {0};
const int n = 60;
void calC()
{
    for (int i = 0; i <= n; i++)
        res[i][0] = res[i][i] = 1;
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= i/2; j++)
        {
            res[i][j] = res[i - 1][j] + res[i - 1][j - 1] % p;
            res[i][i - j] = res[i][j];
        }
    }
}
```

- 方法二

**质因子分解**  
$C_n^m \pmod p=p_1^{c_1}*p_2^{c_2}*...*p_k^{c_k} \pmod p$，可以用快速幂计算每组 $p_i^{c_i}\pmod p$  
需要遍历不超过n的所有质数$p_i$，然后计算 n!、m!、(n-m)!中分别含有质因子$p_i$的个数x、y、z，就知道$C_n^m$中含质因子$p_i$的个数为x-y-z。

```cpp
//使用筛选法得到素数表prime，注意表中最大素数不得小于n
int prime[maxn];
int C(int n, int m, int p)
{
    int ans = 1;
    //遍历不超过n的所有质数
    for (int i = 0; prime[i] <= n; i++)
    {
        //计算c(n,m)中prime[i]的指数c，cal(n,m)为n!中含质因子k的个数
        int c = cal(n, prime[i]) - cal(m, prime[i]) - cal(n - m, prime[i]);
        //快速幂计算prime[i]^c%p
        ans = ans * binaryPow(prime[i], c, p) % p;
    }
}
```

- 方法三
  1. m<p，且p是素数

      ```cpp
      int C(int n, int m, int p)
      {
        int ans = 1;
        for(int i = 1; i <=m; i++)
        {
          ans = ans * (n - m +i) % p;
          ans = ans * inverse(i, p) % p;  //求i的逆元
        }
      }
      ```

  2. m任意，且p是素数----------分母一定存在p的倍数，先处理掉，变量numP统计分子中的p的比分母中的p多几个。

      ```cpp
      int C(int n, int m, int p)
      {
          int ans = 1, numP = 0;
          for (int i = 1; i <= m; i++)
          {
              int temp = n - m + i; //分子
              while (temp % p == 0)
              {
                  numP++;
                  temp /= p;
              }
              ans = ans * temp % p;

              temp = i; //分母
              while (temp % p == 0)
              {
                  numP--;
                  temp /= p;
              }
              ans = ans * inverse(temp, p) % p;
          }
          if (numP > 0)
              return 0;    //若numP>0，直接返回0
          else
              return ans;
      }
      ```

  3. m任意，p可能不是素数----------对p进行质因子分解，针对每一个质因子$p_i$，统计分子比分母中多含质因子$p_i$的个数。

- 方法四(Lucas定理)

如果p是素数，将m和n表示为p进制：$$m=m_kp^k+m_{k-1}p^{k-1}+...+m_0$$ $$n=n_kp^k+n_{k-1}p^{k-1}+...+n_0$$ 那么Lucas定理告诉我们，$C_n^m=C_{n_k}^{m_k}*C_{n_{k-1}}^{m_{k-1}}*...*C_{n_0}^{m_0}$成立

```cpp
int Lucas(int n, int m)
{
    if (m == 0)
        return 1;
    return C(n % p, m % p) * Lucas(n / p, m / p) % p;
}
```

### STL

| vector                                                                                    | stack                                   | queue                      | priority_queue                          |
|-------------------------------------------------------------------------------------------|-----------------------------------------|----------------------------|-----------------------------------------|
| vector\<typename\> name;                                                                  | stack \<typename\> name;                | queue\<typename\> name;    | priority_queue\<typename\> name;        |
| push_back()                                                                               | push(x)                                 | push(x)                    | push(x)                                 |
| pop_back()                                                                                | pop() #需要判断栈是否为空               | pop() #令队首元素出队      | pop() #令队首元素出队                   |
| insert(it, x)                                                                             | top() #栈空时返回-1，需要判断栈是否为空 | front()、back()            | top() #获得队首元素，先判断队列是否为空 |
| erase(it) #it为所需要删除元素的迭代器<br>erase(first, last) #删除[first,last)内的所有元素 | empty()                                 | empty() #检测queue是否为空 | empty() #检测queue是否为空              |
| size() #获得元素的个数                                                                    | size()                                  | size()                     | size()                                  |
| clear() #清空所有元素                                                                     |                                         |                            |                                         |

#### 注意
>
> ##### ① vector
>
> vector\<typename\> name[arraySize] 的一维长度已经固定
> vector\<vector\<typename\>\> name 是两个维都可以变长的二维数组
>
> ##### ② 用栈实现简易计算机
>
> - 中缀表达式转后缀表达式
>
>   - 设立一个操作符栈和一个存放后缀表达式的队列
>
>   - 从左向右扫描中缀表达式，碰到操作数则合并，加入到后缀表达式中
>
>   - 如果碰到操作符op，则与操作符栈的栈顶操作符进行优先级比较
>
>     - op优先级高，则压栈
>
>     - op优先级低或等于，则将操作符栈的操作符不断弹出到后缀表达式中，直到操作符op的优先级高于栈顶操作符的优先级,把op压入栈
>
> - 计算后缀表达式
>
>   - 从左向右扫描,如果是操作数则压入栈,如果是操作符,则连续弹出两个操作数(后弹出的是第一操作数),然后进行操作符操作,生成的新操作数压入栈中
>
> ##### ③ priority_queue
>
> priority_queue队首元素一定是当前队列中优先级最高的那一个。
> 元素优先级设置
> (1)基本数据类型的优先级设置
> 若想把最小的元素放在队首：
> priority_queue\<int, vector\<int\>, greater\<int\>\> q;
> 否则：
> priority_queue\<int, vector\<int\>, less\<int\>\> q;
> (2)结构体的优先级设置
> 重载小于号的友元函数，优先队列的这个重载函数与sort中的cmp函数效果是相反的
>
> ```cpp
> struct fruit{
>     string name;
>     int pricr;
>     friend bool operator < (fruit f1, fruit 2)
>     {
>         return f1.price < f2.price;
>     }
> }
> ```
>
> 或者把重载函数写在结构体外面
>
> ```cpp
> struct cmp{
>     bool operator () (fruit f1, fruit f2)
>     {
>         return f1.price > f2.price;
>     }
> }
> priority_queue<fruit, vector<fruit>, cmp> q;
> ```

| map                                                                                                                                | set                                                                                                                          | string                                                                                                                                                                    | pair                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| map<typename1, typename2> mp;                                                                                                      | set\<typename\> name;                                                                                                        | string str;                                                                                                                                                               | pair<typeName1, typeName2> name;                                                             |
|                                                                                                                                    |                                                                                                                              | substr(pos, len) #返回从pos号位开始，长度为len的字串                                                                                                                      | pair<string, int> p("haha", 5) #用小括号初始化                                               |
|                                                                                                                                    |                                                                                                                              | +=拼接; ==、<、<=、>、>=按字典序比较大小                                                                                                                                  | 使用==、<、<=、>、>=比较大小，规则以先first的大小为标准，只有当first相等时才去判断second大小 |
|                                                                                                                                    | inset(x)                                                                                                                     | insert(pos, string) #在pos号位置插入字符串string<br>insert(it, it2, it3) #it为原字符串的欲插入位置，it2和it3为待插字符串的首位迭代器，将串[it2, it3)插在it的位置上        | pair<string, int>("haha", 5) #构建临时pair<br>make_pair("haha", 5) #构建临时pair             |
| find(key) #返回键为key的映射的迭代器                                                                                               | find(value) #返回set中对应值为value的迭代器,若找不到，返回end迭代器                                                          | str.find(str2, pos) #从str的pos位开始匹配str2，返回str中第一次出现的位置，若找不到，返回string::npos                                                                      | pair只有两个元素，分别是first和second                                                        |
| erase(it)<br> #it为所需要删除元素的迭代器<br>erase(key) #key为欲删除的映射的键<br>erase(first, last) #删除[first,last)内的所有元素 | erase(it) #it为所需要删除元素的迭代器<br>erase(first, last) #删除[first,last)内的所有元素<br>erase(value) #删除值为value元素 | erase(it)<br> #it为所需要删除元素的迭代器<br>erase(first, last) #删除[first,last)内的所有元素<br>erase(pos, length)  #pos为需要开始删除的起始位置，length为删除的字符个数 |                                                                                              |
| size()                                                                                                                             | size()                                                                                                                       | length()/size()                                                                                                                                                           |                                                                                              |
| clear()                                                                                                                            | clear()                                                                                                                      | clear()                                                                                                                                                                   |                                                                                              |

#### 注意

> ①用c_str()将string类转换为字符数组，可以用printf输出,printf("%s\n", str.c_str());
>
> ②pair 可以作为map的键值对来进行插入
>
> ```cpp
> map<string, int> mp;
> mp.insert(make_pair("heihei", 5));
> mp.insert(pair<string, int>("haha", 10));
> for(map<string, int>::iterator it = mp.begin(); it != mp.end(); it++)
> {
>     cout << it->first << " " << it->second << endl;
> }
> ```

#### 链表

##### 使用malloc函数或者new运算符为链表结点分配内存空间

```c
    #include <stdlib.h>
    typename* p = (typename*)malloc(sizeof(typename)); //若申请失败,则返回空指针NULL
    free(p); //释放资源,将指针p指向NULL
```

```cpp
    typename* p = new typename; //若申请失败,则会启动C++异常机制处理
    delete(p); //释放资源,防止内存泄漏
```

### algorithm

- reverse(it, it2)可以将数组指针在[it, it2)之间的元素或容器的迭代器在[it, it2)范围内的元素进行反转
- next_permulation()给出一个序列在全排列中的下一个序列，eg:231的下一个序列是312，再下一个是321
- fill()可以把数组或容器中的某一段区间赋为某个相同的值
- sort(首元素地址(必填), 尾元素地址的下一个地址(必填), 比较函数(非必填));
- lower_bound(first, last, val)用在一个有序数组或容器中，寻找[first, last)范围内第一个值大于等于val的元素的位置，如果数组，则返回该位置的指针，如果是容器，则返回该位置的迭代器
- upper_bound(first, last, val)用在一个有序数组或容器中，寻找[first, last)范围内第一个值大于val的元素的位置，如果数组，则返回该位置的指针，如果是容器，则返回该位置的迭代器

### 树

#### 二叉树的基本操作

##### 存储结构

```cpp
struct node
{
    typename data; //数据域
    node *lchild;
    node *rchild;
};
```

##### 建立新结点

```cpp
node *newNode(int v)
{
    node *Node = new node;
    Node->data = v;
    Node->lchild = Node->rchild = NULL;
    return Node;
}
```

##### 查找与修改

```cpp
void search(node *root, int x, int newdata)
{
    if (root == NULL)
    {
        return;
    }
    if (root->data == x)
    {
        root->data = newdata;
    }
    search(root->lchild, x, newdata);
    search(root->rchild, x, newdata);
}
```

##### 结点插入

```cpp
void insert(node *&root, int x) //root使用了引用，在函数中修改root会直接修改原变量
{
    if (root == NULL)
    {
        root = newNode(x);
        return;
    }
    if (由二叉树的性质，x应该插在左子树)
    {
        insert(root->lchild, x);
    }
    else
    {
        insert(root->rchild, x);
    }
}
```

##### 二叉树的创建

```cpp
node *Creat(int data[], int n)
{
    node *root = NULL;
    for (int i = 0; i < n; i++)
    {
        insert(root, data[i]);
    }
    return root;
}
```

##### 通过先序序列与中序序列构建二叉树

```cpp
node *create(int preL, int preR, int intL, int intR)
{
    if (preL > preR)
    {
        return NULL;
    }
    node *root = new node;
    root->data = pre[preL];
    int k;
    for (k = inL; k <= inR; k++)
    {
        if (in[k] == pre[prel])
            break;
    }
    int numLeft = k - inL;
    root->lchild = create(preL + 1, preL + numLeft, inL, k - 1);
    root->rchild = create(preL + numLeft + 1, preR, k + 1, inR);
    return root;
}
```

#### 二叉查找树

① 要么二叉查找树是一棵空树
② 要么二叉查找树由根结点、左子树、右子树组成，其中左子树和右子树都是二叉查找树，且左子树上所有结点的数据域均小于或等于根结点的数据域，右子树上所有结点的数据域均大于根结点的数据域

##### 删除操作

①如果当前结点root为空，说明不存在权值为给定权值x的结点，直接返回
②如果当前结点root的权值恰为给定的权值x，说明找到了想要删除的结点，此时进入删除处理
a)如果当前结点root不存在左右孩子，说明是叶子结点，直接删除
b)如果当前结点root存在左孩子，那么在左子树中寻找前驱pre，然后让pre的数据覆盖root，接着在左子树中删除结点pre
c)如果当前结点root存在右孩子，那么在右子树中寻找结点后继next，然后让next的数据覆盖root，接着删除结点next
③如果当前结点root的权值大于给定的权值x，则在左子树中递归删除权值为x的结点
④如果当前结点root的权值小于给定的权值x，则在右子树中递归删除权值为x的结点
注意：这是一个递归删除结点的过程

#### 平衡二叉树

AVL树仍然是一棵二叉查找树，其左子树与右子树的高度之差的绝对值不超过1

##### 左旋

![左旋](suanfa_md_files/%E5%B7%A6%E6%97%8B.PNG?v=1&type=image)

##### 右旋

![右旋](suanfa_md_files/%E5%8F%B3%E6%97%8B.png?v=1&type=image)

##### LR调整

![LR调整](suanfa_md_files/LR%E8%B0%83%E6%95%B4.PNG?v=1&type=image)

##### RL调整

![RL调整](suanfa_md_files/RL%E8%B0%83%E6%95%B4.PNG?v=1&type=image)

##### 插入结点

```cpp
void insert(node *&root, int v)
{
    if (root == NULL)
    {
        root = newNode(v);
        return;
    }

    if (v < root->v)
    {
        insert(root->lchild, v);
        updateHeight(root);
        if (getBalanceFactor(root) == 2)
        {
            if (getBalanceFactor(root->lchild) == 1) //LL型
            {
                R(root);
            }
            else if (getBalanceFactor(root->lchild) == -1) //LR型
            {
                L(root->lchild);
                R(root);
            }
        }
    }
    else
    {
        insert(root->rchild, v);
        updateHeight(root);
        if (getBalanceFactor(root) == 2)
        {
            if (getBalanceFactor(root->rchild) == -1) //RR型
            {
                L(root);
            }
            else if (getBalanceFactor(root->rchild) == 1) //RL型
            {
                RL(root->lchild);
                L(root);
            }
        }
    }
}
```

#### 并查集

①合并：合并两个集合
②查找：判断两个元素是否在一个集合

> int father[N]
> father[i]表示元素i的父亲结点
> 如果father[i]==i，则说明元素i是该集合的根结点

##### 基本操作

- 初始化，每个元素都是独立的一个集合

```cpp
for(int i = 1; i <=N; i++)
{
    father[i] = i;
}
```

- 查找，由于规定同一个集合中只存在一个根结点，因此查找操作就是对给定的结点寻找其根结点的过程

```cpp
int findFather(int x){
    while(x != father[x]){
        x = father[x];
    }
    return x;
}
```

- 合并

```cpp
void Union(int a, int b){
    int faA = findFather(a);
    int faB = findFather(b);
    if(faA != faB){
        father[faA] = faB;
    }
}
```

##### 路径压缩

把当前查询结点的路径上的所有结点的父亲都指向根结点

```cpp
int findFather(int v){
    if(v == father[v]) return v;
    else{
        int F = findFather(father[v]);
        father[v] = F;
        return F;
    }
}
```

#### 堆

##### 向下调整

```cpp
void downAdjust(int low, int high)
{
    //对heap数组在[low, high]范围进行向下调整
    //其中low为欲调整结点的数组下标，high一般为堆的最后一个元素的数组下标
    int i = low, j = i * 2;
    while (j <= high) //存在孩子结点
    {
        if (j + 1 <= high && heap[j + 1] > heap[j])
        {
            j = j + 1;//让j存储右孩子的下标
        }
        //如果孩子中最大的权值比欲调整结点i大
        if (heap[j] > heap[i])
        {
            swap(heap[j], heap[i]);
            i = j;
            j = i * 2;
        }
        else
        {
            break;
        }
    }
}
```

##### 建堆

```cpp
void createHeap()
{
    for(int i = n / 2; i>=1; i--)
        downAdjust(i, n);
}
```

##### 删除堆顶元素

```cpp
void deleteTop()
{
    heap[1] = heap[n--];
    downAdjust(1, n);
}
```

##### 向上调整

```cpp
void upAdjust(int low, int high)
{
    int i = high, j = i / 2;
    while (j >= low)
    {
        if (heap[j] < heap[i])
        {
            swap(heap[j], heap[i]);
            i = j;
            j = i / 2;
        }
        else
        {
            break;
        }
    }
}
```

##### 添加元素x

```cpp
void insert(int x)
{
    heap[++n] = x;
    upAdjust(1, n);
}
```

##### 堆排序

```cpp
void heapSort()
{
    createHeap();
    for(int i = n; i > 1; i--)
    {
        swap(heap[i], heap[1]);
        downAdjust(1, i-1);
    }
}
```

#### 哈夫曼树

> 不存在度为1的结点
> 可以使用优先队列

### 图

#### 图的存储

##### 邻接矩阵

> 如果G[i][j]为1，则说明顶点i和顶点j之间有边
> 如果存在边权，则可以令G[i][j]存放边权，对不存在的边可以设边权为0、-1或是一个很大的数

##### 邻接表

```cpp
struct Node{
    int v;  //边的终点编号
    int w;  //边权
};
vector<Node> Adj[N];
```

#### 图的遍历

##### 深度优先搜索(DFS)法

```cpp
DFS(u)  //访问顶点u
{
    vis[u] = true;  //设置u已被访问
    for(从u出发能到达的所有顶点)    //枚举从u出发可以到达的所有顶点v
        if vis[v] == false;     //如果v未被访问
            DFS(v);     //递归访问v
}

DFSTrave(G) //遍历图G
{
    for(G的所有顶点u)
        if vis[u] == false
            DFS(u);     //访问u所在的连通块
}
```

##### 广度优先搜索(BFS)法

```cpp
BFS(u){
    queue q;    //定义队列q
    inq[u] = true;  //设置u已被加入过队列
    while(q非空){   //只要队列非空
        取出q的队首元素u进行访问;
        for(从u出发可达的所有顶点v)     //枚举从u能直接到达的顶点v
            if(inq[v] == false){    //如果v未曾加入过队列
                将v入队;
                inq[v] = true;      //设置v已被加入过队列
            }

    }
}

BFSTrave(G){    //遍历图G
    for(G的所有顶点u)     //枚举G的所有顶点u
        if(inq[u] == false){    //如果u未曾加入过队列
            BFS(u);     //遍历u所在的连通块
        }
}
```

#### 最短路径

```cpp
Dijkstra(G, d[], s){
    初始化;
    for(循环n次){
        u = 使d[u]最小的还未被访问的顶点的标号;
        记u已被访问;
        for(从u出发能到达的所有顶点v){
            if(v未被访问&&以u为中介点使s到顶点v的最短距离d[v]更优){
                优化d[v];
                令v的前驱为u;
            }
        }
    }
}

//知道每个顶点的前驱，获得路径
void DFS(int s, int v){ //s为起点编号，v为当前访问的顶点编号
    if(v == s){
        printf("%d\n", s);
        return;
    }
    DFS(s, pre[v]);
    printf("%d\n", v);
}
```

##### 新增边权

以新增的边权代表花费为例，用cost[u][v]表示u→v的花费，并增加一个数组c[]，令从起点s到达顶点u的最少花费为c[u]，初始化c[s]为0，其余c[u]均为INF。

```cpp
for(int v =0; v < n; v++){
    //如果v未访问&&u能到达v
    if(vis[v] == false && G[u][v] != INF){
        if(d[u] + G[u][v] < d[v]){  //以u为中介点可以使d[v]更优
            d[v] = d[u] + G[u][v];
            c[v] = c[u] + c[u][v];
        } else if(d[u] + G[u][v] == d[v] && c[v] > c[u] + c[u][v]){
            c[v] = c[u] + c[u][v];
        }
    }
}
```

##### 新增点权

以新增点权代表城市中能收集到的物资为例，用weight[u]表示城市u中的物资数目，并增加一个数组w[]，令从起点s到顶点u可以收集到的最大物资为w[u]，初始化w[s]为weight[s]，其余w[u]均为0。

```cpp
for(int v =0; v < n; v++){
    //如果v未访问&&u能到达v
    if(vis[v] == false && G[u][v] != INF){
        if(d[u] + G[u][v] < d[v]){  //以u为中介点可以使d[v]更优
            d[v] = d[u] + G[u][v];
            c[v] = c[u] + c[u][v];
        } else if(d[u] + G[u][v] == d[v] && weight[v] < weight[u] + weight[u][v]){
            weight[v] < weight[u] + weight[u][v];
        }
    }
}
```

##### 求最短路径条数

只需要增加一个数组num[]，令从起点s到达顶点u的最短路径条数为num[u]，初始化时只有num[s]为1，其余num[u]均为0。在 d[u] + G[u][v] < d[v] 时更新d[v]，并让num[v]继承num[u]，而当 d[u] + G[u][v] == d[v] 时将num[u]加到num[v]上。

##### 可以 Dijkstra+DFS

```cpp
//1、使用Dijkstra算法记录所有最短路径
vector<int> pre[maxv];

void Dijkstra(int s)
{
    fill(d,d+maxv,INF);
    d[s]=0;
    for(int i=0;i<n;++i)
    {
        int u=-1;min=INF;
        for(int j=0;j<n;++j)
        {
            if(vis[j]==false&&d[j]<min)
            {
                u=j;
                min=d[j];
            }
        }
        if(u==-1)
            return ;
        vis[u]=true;
        for(int v=0;v<n;++v)
        {
            if(vis[v]==false&&G[u][v]!=INF)
            {
                if(d[u]+G[u][v]<d[v])
                {
                    d[v]=d[u]+G[u][v];//优化d[v]
                    pre[v].clear(); //清空pre
                    pre[v].push_back(u); //记录v的前驱u
                }
                else if(d[u]+G[u][v]==d[v])
                    pre[v].push_back(u); //记录v的前驱u
            }
        }
        }
}

//2、遍历所有最短路径，找出一条使第二标尺最优的路径。
//DFS 递归函数
//1.1 作为记录第二尺度最优值的全局变量optvalue
//1.2 记录最优路径的数组path（vector实现）
//1.3 记录遍历到叶子结点时的路径，temppath（vector）

int optvalue; //第二尺度最优值
vector <int> pre[maxv];
vector<int> path,temppath;
void DFS(int v) //v为当前访问结点
{
    if(v==st) //递归边界，如果到达了叶子结点st，即路径的起点
    {
        temppath.push_back(v);//将起点st加入临时路径temppath最后面
        int value; //记录临时路径temppath的第二标尺的值
        计算路径temppath上的value值；
        if(value优于optvalue)
        {
            optvalue=value;
            path=temppath;
        }
        temppath.pop_back(); //将刚加入的结点删除
        return;
    }
    //递归式
    temppath.push_back(v); //将当前访问结点加入临时路径temppath最后面
    for(int i=0;i<pre[v].size();++i)
        DFS(pre[v][i]); //结点v的前驱结点pre[v][i],递归
    temppath.pop_back(); //遍历完所有前驱结点，将当前结点v删除
}

//3、计算temppath上边权和点权之和
//边权之和  
int value=0;
//由于递归的原因，temppath中的结点是逆序的。固应倒着访问结点，循环条件为i>0
for(int i=temppath.size()-1;i>0;--i)
{
    //当前结点为id，下一个结点为idnext；
    int id=temppath[i],idnext=temppath[i-1];
    value+=v[id][idnext]; //value值累加边id->idnext 的边权
}
// 点权之和计算方法
int value =0;
for(int i=temppath.size()-1;i>=0;--i) //倒着访问结点，循环条件为i>=0
{
    //当前结点为id
    int id=temppath[i];
    value+=w[id]; //value值累加结点id 的点权
}  
```

##### Bellman-Ford算法

```cpp
//松弛操作
for(int i = 0; i < n - 1; i++){ //执行n-1轮操作，其中n为顶点数
    for(each edge u->v){    //每轮操作都遍历所有边
        if(d[u] + length[u->v] < d[v]){ //以u为中介点可以使d[v]更小
            d[v] = d[u] + length[u->v]; //松弛操作
        }
    }
}

//判断负环
for(each edge u->v){    //对每条边进行判断
    if(d[u] + length[u->v] < d[v]){ //如果仍可以被松弛
        return false;   //说明图中有从源点可达的负环
    }
}
return true;
```

##### SPFA算法

改进Bellman-Ford算法：只有当某个顶点u的d[u]值改变时，从它出发的边的邻接点v的d[v]值才可能被改变

```cpp
queue<int> Q;
源点 s 入队;
while(队列非空){
    取出队首元素u;
    for(u的所有邻接边u->v){
        if(d[v] > d[u] + dis){
            d[v] = d[u] + dis;
            if(v当前不在队列){
                v入队;
                if(v入队次数大于n-1){
                    说明有可达负环,return;
                }
            }
        }
    }
}
```

##### Floyd算法

```cpp
枚举顶点 k ∈ [1, n]
    以顶点k作为中介点，枚举所有顶点对i和j(i ∈ [1, n], j ∈ [1, n])
        如果 dis[i][k] + dis[k][j] < dis[i][j] 成立
            赋值dis[i][j] = dis[i][k] + dis[k][j]
```

#### 最小生成树

##### prim算法

```cpp
Prim (G, d[]){  //d[]含义为顶点Vi与集合S的最短距离
    初始化;
    for(循环n次){
        u = 使d[u]最小的还未被访问的顶点的标号;
        记u已被访问;
        for(从u出发能到达的所有顶点v){
            if(v未被访问&&以u为中介使得v与集合s的距离d[v]更优){
                将G[u][v]赋值给v与集合s的最短距离d[v]；
            }
        }
    }
}
```

##### Kruskal算法

```cpp
int Kruskal(){  //可以用并查集实现
    令最小生成树的边权之和为ans、最小生成树的当前边数Num_Edge;
    将所有边按边权从小到大排序;
    for(从小到大枚举所有边){
        if(当前测试边的两个端点在不同的连通块中){
            将该测试边加入最小生成树中;
            ans += 测试边的边权;
            最小生成树的当前边数 Num_Edge 加1;
            当边数 Num_Edge 等于顶点数减1时结束循环;
        }
    }
    return ans;
}
```

如果是稠密图(边多),则用prim算法;如果是稀疏图(边少),则用kruskal算法

#### 拓扑排序

1. 定义一个队列Q，并把所有入度为0的结点加入队列。

2. 取队首结点，输出。然后删去所有从它出发的边，并令这些边到达的顶点的入度减1，如果某个顶点的入度减为0，则将其加入队列。

3. 反复进行②操作，直到队列为空。如果队列为空时入过队的结点数目恰好为N，说明拓扑排序成功，否则失败。
