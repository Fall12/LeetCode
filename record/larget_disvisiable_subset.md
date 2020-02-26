# [368. 最大整除子集](https://leetcode-cn.com/problems/largest-divisible-subset/)

###题意
给出一个由无重复的正整数组成的集合，找出其中最大的整除子集，子集中任意一对 (Si，Sj) 都要满足：Si%Sj=0 或 Sj%Si=0。

如果有多个目标子集，返回其中任何一个均可。

示例 1:

输入: [1,2,3]  
输出: [1,2] (当然, [1,3] 也正确)

###思路
先排序，dp[i]记录位置nums[i]可以整除的最大个数
pre[i]记录链接到哪个位置
### 代码
```cgo
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        vector<int> ans;
        if(nums.size()<=0) return ans;
        sort(nums.begin(), nums.end());
        vector<int> dp(nums.size(), 1);
        vector<int> pre(nums.size(), -1);
        int maxLen =1, maxIndex=0;
        for(int i=1; i<nums.size(); i++){
            for(int j=i-1; j>=0; j--){
                if(nums[i]%nums[j]==0) {
                    if(dp[i] < dp[j]+1) {
                        dp[i] = dp[j] +1;
                        pre[i] = j;
                    }
                }
            }
            if(dp[i] > maxLen) {
                maxLen= dp[i];
                maxIndex = i;
            }
        }
        while(pre[maxIndex] != -1) {
            ans.insert(ans.begin(), nums[maxIndex]);
            maxIndex= pre[maxIndex];
        }
        ans.insert(ans.begin(), nums[maxIndex]);
        return ans;
    }
```

