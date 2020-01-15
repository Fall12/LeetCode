# [338. 比特位计数](https://leetcode-cn.com/problems/counting-bits/)

### 题意
给定一个非负整数num。对于0≤i≤num范围中的每个数字i，计算其二进制数中的1的数目并将它们作为数组返回。

示例 1:

输入: 2
输出: [0,1,1]

### 思路
来自题解  

奇数：二进制表示中，奇数一定比前面那个偶数多一个1，因为多的就是最低位的1。  
偶数：二进制表示中，偶数中1的个数一定和除以2之后的那个数一样多。因为最低位是0，除以2就是右移一位，也就是把那个0抹掉而已，所以1的个数是不变的。
 
### 代码

```cgo
    vector<int> countBits(int num) {
      vector<int> dp(num+1);
      dp[0] = 0;
      for(int i=0; i<=num; i++){
          if(i%2 == 1) dp[i] = dp[i-1]+1;
          else dp[i] = dp[i/2];
      }
      return dp;  
    }
```
