# [516. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

### 题意
给定一个字符串s，找到其中最长的回文子序列。可以假设s的最大长度为1000。

### 思路
求原串与逆序串的最长公共子序列

### 代码
```cgo
    int max(int a, int b) { 
        if(a > b) return a;
        return b;
    }
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        vector<vector<int>> dp(n+1, vector<int>(n+1, 0));
        for(int i=1;i<=n;i++) {
            for(int j=1; j<=n; j++) {
                if(s[i-1] == s[n-j]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                } else {
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        return dp.at(n).at(n);
    }
```