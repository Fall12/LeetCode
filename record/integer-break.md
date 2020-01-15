# [343. 整数拆分](https://leetcode-cn.com/problems/integer-break/)
### 题意
给定一个正整数n，将其拆分为至少两个正整数的和，并使这些整数的乘积最大化。返回你可以获得的最大乘积。

示例 1:

输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
### 思路
贪心  
易推出：大数字都可以被拆分为多个小因子，以获取更大的乘积，只有2和3不需要拆分。
### 代码
```cgo
    int integerBreak(int n) {
       if(n==2) return 1;
       if(n==3) return 2;
       if(n==4) return 4;
       int ans = 1;
       ans = dfs(n);
       return ans;
    }
    int dfs(int n) {
        if(n==1 || n ==2 || n ==3 || n ==4) return n;
        return 3*dfs(n-3);
    }
```