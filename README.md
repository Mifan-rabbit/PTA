# PAT
## [1001 A+B Format ](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)[(20分)](https://github.com/Mifan-rabbit/PTA/blob/master/1001%20A%2BB%20Format%20(20%E5%88%86).md)
- 六位数相加减，结果是可以枚举的，共三种：①A; ②A,B; ③A,B,C;
- 直接输出时，若结果为1000，则输出为1,0，故需要格式化输出
- 一开始的解题思路是使用vector，每模1000，就压入vector，但欠考虑和为0时，vector为空

## [1002 A+B for Polynomials ](https://pintia.cn/problem-sets/994805342720868352/problems/994805526272000000)[(25分)]()
- 声明变量时注意变量类型，exponents(指数)为整数，coefficients(系数)为浮点数
- 循环注意次数及范围
  - K  N1  aN1  N2  aN2  ...  Nk  aNk 
  - 1 ≤ K ≤ 10 => 最多有十个数系数不为零
  - 0 ≤ Nk ≤ ... ≤ N2 ≤ N1 ≤ 1000 =>指数的范围

# LeetCode
## [1163. Last Substring in Lexicographical OrderHard](https://leetcode.com/problems/last-substring-in-lexicographical-order/)
- C++ String的使用 
  1. 截取子串
  
    |函数||
    | :---- | :---- |
    | s.substr(pos, n) | 截取s中从pos开始（包括0）的n个字符的子串，并返回 |
    | s.substr(pos)    | 截取s中从从pos开始（包括0）到末尾的所有字符的子串，并返回 |

  2. 替换子串

    |函数||
    | :---- | :---- |
    | s.replace(pos, n, s1)) | 用s1替换s中从pos开始（包括0）的n个字符的子串 |
  
  3. 查找子串

    |函数||
    | :---- | :---- |
    | s.find(s1)| 查找s中第一次出现s1的位置，并返回（包括0）|
    | s.rfind(s1)| 查找s中最后次出现s1的位置，并返回（包括0）|  
    | s.find_first_of(s1)| 查找在s1中任意一个字符在s中第一次出现的位置，并返回（包括0）|
    | s.find_last_of(s1)| 查找在s1中任意一个字符在s中最后一次出现的位置，并返回（包括0）|
    | s.fin_first_not_of(s1)| 查找s中第一个不属于s1中的字符的位置，并返回（包括0）|
    | s.fin_last_not_of(s1)| 查找s中最后一个不属于s1中的字符的位置，并返回（包括0）|  
  
- 解题边界问题
    1. 按字典顺序，可以通过比较字符的大小得出，但在当输入为 4\*10^5 个相同字符时，会有可能超时
    2. 我的想法是，按字符串顺序搜索字典序列最大的字母，若遇到大小相同的字符，就依次比较其后跟字符大小，这时会有三种情况：
        1. 出现比子串开头更大的字母，则改变子串开头字符，从这个字符开始继续搜索
        2. 后跟字符不相等，选择后跟字符大的，继续搜索
        3. 其中一个遍历到字符串末尾，则最大子串已经找到

## [1025 PAT Ranking (25分)](https://pintia.cn/problem-sets/994805342720868352/problems/994805474338127872)
- sort函数
  - 头文件 #include<algorithm>
  - 方式 sort(首元素地址, 尾元素地址的下一个地址, 比较函数(非必填))
  
- strcmp函数
  - 头文件 string.h
  - 方式 strcmp(str1, str2)
    - 当str1的字典顺序小于str2时返回一个负数，注意，这个负数不一定是-1，具体和编译器相关
 
- 实现排名
  - 分数不同排名不同，分数相同排名相同，且占用一个排位
  - ```
    stu[0]=1;
    for(int i=1; i<num; ++i)
    {
      if(stu[i].score == stu[i-1].score)
        stu[i].rank = stu[i-1].rank;
      else
        stu[i].rank = i+1;
     }
    ```
