# PTA
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
