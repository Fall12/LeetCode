# [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

### 题意
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:
``` 
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为6。
```

### 代码
```cgo
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums.at(0);
        int curSum = maxSum;
        for(int i=1; i<nums.size(); i++) {
            if (curSum<0) {
                curSum = nums.at(i);
            } else {
                 curSum+= nums.at(i);
            }  
            if (curSum > maxSum) {
                maxSum = curSum;
            }
        }

        return maxSum;
    }
};
```