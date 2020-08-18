# 1001 A+B Format (20分)
Calculate a+b and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

## Input Specification:
Each input file contains one test case. Each case contains a pair of integers a and b where −10
​6
​​ ≤a,b≤10
​6
​​ . The numbers are separated by a space.

## Output Specification:
For each test case, you should output the sum of a and b in one line. The sum must be written in the standard format.

## Sample Input:
-1000000 9

## Sample Output:
-999,991

## Code
```cpp
#include<iostream>
using namespace std;

int main(){
    int a,b;
    cin>>a>>b;
    a+=b;
    
    if(a<0)
    {
        cout<<'-';
        a=-a;
    }
    
    if(a>=1000000)
        printf("%d,%03d,%03d",a/1000000,a%1000000/1000,a%1000);
    else if(a>=1000)
        printf("%d,%03d",a/1000,a%1000);
    else
        printf("%d",a);
    
    return 0;
}
```

## 坑
- 六位数相加减，格式化后的结果是可以枚举的
- 直接输出时，若结果为1000，则输出为1,0，故需要格式化输出
- 一开始的解题思路是使用vector，每模1000，就压入vector，但欠考虑和为0时，vector为空
