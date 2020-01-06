# [139. 单词拆分](https://leetcode-cn.com/problems/word-break/)

### 题意
给定一个非空字符串s和一个包含非空单词列表的字典wordDict，判定s是否可以被空格拆分为一个或多个在字典中出现的单词。  

说明：

拆分时可以重复使用字典中的单词。
你可以假设字典中没有重复的单词。
示例 1：

输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。

### 思路
s = "leetcode", wordDict = ["leet", "code"] 
dp[n]代表从开始到n可以被拆分。 假如d[7]要可以被拆分，那么，dp[n-k]也必须是可以被拆分的。k是某个单词的长度。

### 代码
```cgo

    bool wordBreak(string s, vector<string>& wordDict) {
        int n=s.size();
        if(n <=0 ) return true;
        vector<bool> dp(n, false);
        for(int i=0; i<n; i++) {
            if(i == 0 || (i>0 && dp[i-1])) {
                for(int j=0;j<wordDict.size(); j++) {
                    int k =0;
                    for(; k<wordDict[j].size(); k++) {
                        if(k+i >= n || wordDict[j][k] != s[i+k]) break;
                    }

                    if(k==wordDict[j].size()) dp[i+k-1] = true;
                }
            }
            if(dp[n-1]) return true;
        }
        return dp[n-1];
    }
```