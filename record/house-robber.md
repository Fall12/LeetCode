# [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)
### 题意
[1,2,3,1] 求和的最大值，但不能有相邻的数相加
### 思路
dp[i] 代表在位置i能得到最大的和
更新过程， dp[i] = max{dp[i-2]+ num[i-1], dp[i-1]}

### 代码
```cgo
    int rob(vector<int>& nums) {
        if(nums.size() <=0 )return 0;
        vector<int> dp(nums.size()+1, 0);
        dp[1]= nums[0];
        for(int i=2; i<=nums.size(); i++){
            dp[i]= dp[i-2]+nums[i-1];
            if(dp[i]<dp[i-1]) dp[i] = dp[i-1];
        }
        return dp[nums.size()];
    }
```