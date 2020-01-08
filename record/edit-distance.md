# [72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)

### 题意
给定两个单词word1和word2，计算出将word1转换成word2所使用的最少操作数。  
你可以对一个单词进行如下三种操作：  

插入一个字符
删除一个字符
替换一个字符
示例 1:

输入: word1 = "horse", word2 = "ros"
输出: 3
解释: 
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')

### 思路
来源题解  
第一个单词的前i位变成第二个单词的前j-1位，然后再插入一个字符（d[i][j-1]+1）  
第一个单词的前i-1位变成第二个单词的前j位，然后再删去一个字符（d[i-1][j]+1）  
第一个单词的前i-1位变成第二个单词的前j-1位，然后替换最后一个字符，如果最后一个字符相同，即第一个单词的第i位和第二个单词的第j位相同的话，就不用替换了（d[i-1][j-1]），反之，如果不同就替换最后一位（d[i-1][j-1]+1）  

### 代码
```cgo
    int min(int a,int b) {
        if(a < b) return a;
        return b;
    }
    int minDistance(string word1, string word2) {
        int n=word1.size(), m=word2.size();
        vector<vector<int>> dp(n+1, vector<int>(m+1));
        for(int i=0; i<=n; i++) dp[i][0] = i;
        for(int j=0; j<=m; j++) dp[0][j] = j;
        for(int i=1; i<=n; i++) 
           for(int j=1; j<=m; j++) {
               if(word1[i-1] == word2[j-1]) {
                   dp[i][j]= dp[i-1][j-1];
               }else {
                   dp[i][j] = min(min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) + 1;
               }
           }
        return dp[n][m];
    }
```