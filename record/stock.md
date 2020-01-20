# [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)
### 题意
给定一个数组，它的第i个元素是一支给定股票第i天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。
### 代码
```cgo
    int maxProfit(vector<int>& prices) {
        int profit=0, min=INT_MAX;
        for(int i=0; i<prices.size(); i++){
            if(prices[i]<min) {
                min = prices[i];
            }
            if(prices[i]-min> profit) profit = prices[i]-min;
        }
        return profit;
    }
```
# [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)
### 题意
给定一个数组，它的第i个元素是一支给定股票第i天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
### 代码
```cgo
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        int count =0;
       // vector<int> dp(n,0)
        for(int i=1; i<n; i++){
            if(prices[i]>=prices[i-1]) count += prices[i]-prices[i-1];
        } 
        return count;
    }
```
# [123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)
### 题意
给定一个数组，它的第i个元素是一支给定的股票在第i天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成两笔交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
### 思路
来自题解： 两路dp, dp1[i]表示从[0,i]做一次买卖的最大收益, dp2[i]表示从[i,size]做一次的最大收益, max(dp1[i]+dp2[i])即为做两次的最大收益
### 代码
```cgo
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        if(n<=0) return 0;
        vector<int> dp(n, 0);
        int min=prices[0], max_val=0;
        for(int i=1; i<n; i++) {
            int current = prices[i] - min;
            if(current > max_val ) max_val= current;
            if(prices[i]< min) min = prices[i];
            dp[i] = max_val;
        }

        vector<int> reDp(n, 0);
        int max= prices[n-1];
        max_val = 0;
        for(int i=n-1; i>=0; i--){
            int current = max- prices[i];
            if(current > max_val) max_val= current;
            if(prices[i]>max) max = prices[i];
            reDp[i] = max_val;
        }
        max =dp[n-1];
        for(int i=1; i<n-1;i++){
            int current = dp[i-1] + reDp[i];
            if(current > max) max = current;
        }
        return max;
    }
    }
```

