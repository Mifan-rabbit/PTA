# PTA
## [1001 A+B Format (20分)](https://github.com/Mifan-rabbit/PTA/blob/master/1001%20A%2BB%20Format%20(20%E5%88%86).md)
- 六位数相加减，格式化后的结果是可以枚举的
- 直接输出时，若结果为1000，则输出为1,0，故需要格式化输出
- 一开始的解题思路是使用vector，每模1000，就压入vector，但欠考虑和为0时，vector为空
