# [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring)

### 题意
给定一个字符串s，找到s中最长的回文子串。你可以假设s的最大长度为1000。

### 思路
采用中心扩展法
共有有2n-1个点

### 代码
```cgo
    string longestPalindrome(string s) {
        string ans;
        if (s.size() <= 0) {
            return "";
        }
        int left=0, right =0;
        int maxLen = -1;
        for(int i=0; i<s.size(); i++){
            int len1 = palindromeLen(s, i, i);
            int len2 = palindromeLen(s, i, i+1);
            int len = len1 > len2 ? len1: len2;
            if(len > maxLen) {
                int flag = len%2<1 ? 1:0;
                maxLen = len;
                left = i- len/2 + flag;
                right = i+len/2;
            }
        }
        return ans.assign(s, left, right-left+1);
    }

    int palindromeLen(string s,int left, int right) {
        while(left>=0 && right< s.size() && s[left] == s[right]) {
            left --;
            right ++;
        }
        return right-left-1;
    }
```