# [120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

### 题意
给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。
例如，给定三角形：
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

### 代码
内存O(n)版
```cgo
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int dp[triangle.size()+1];
        for(int i=0; i<triangle.size()+1; i++) dp[i] = 0;

        for(int i=triangle.size()-1; i>=0; i--) {
            vector<int> curV = triangle.at(i);
            for(int j=0; j<curV.size(); j++) {
                int min = dp[j] < dp[j+1] ? dp[j]:dp[j+1];
                dp[j] = min+curV.at(j);
            }
        }

        return dp[0];
    }
};
```