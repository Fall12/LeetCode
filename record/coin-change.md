# [322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

### 题意
给定不同面额的硬币coins和一个总金额amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回-1。

示例 1:
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1

### 思路
dp[i] 代表金额为i所需最少的硬币个数

### 代码
```cgo
    int coinChange(vector<int>& coins, int amount) {
        vector<int>dp(amount+1, -1);
        dp[0] = 0;
        for(int i=1; i<= amount; i++){
            int min = INT_MAX;
            for(int j=0; j<coins.size(); j++) {
                int newIndex= i-coins[j];
                if(newIndex>=0 && dp[newIndex] >=0) {
                    int newMin = dp[newIndex]+1;
                    if(newMin<min) min = newMin;
                }
            }
            if(min < INT_MAX) dp[i]=min;
        }
        return dp[amount];
    }

```