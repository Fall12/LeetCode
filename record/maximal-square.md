# [221. 最大正方形](https://leetcode-cn.com/problems/maximal-square/)

### 题意
在一个由0和1组成的二维矩阵内，找到只包含1的最大正方形，并返回其面积。  
示例:    
输入:   
1 0 1 0 0  
1 0 1 1 1  
1 1 1 1 1  
1 0 0 1 0    
输出: 4

### 思路
dp[i][j]=min(dp[i-1][j], min(dp[i-1][j-1], dp[i][j-1])) + 1;

### 代码
```cgo
    int min(int a,int b) {
        if(a<b) return a;
        return b;
    }
    int maximalSquare(vector<vector<char>>& matrix) {
        int n=matrix.size();
        if(n <= 0) return 0;
        int m=matrix[0].size();
        int max = 0;
        vector<vector<int>> dp(n, vector<int>(m));
        for(int i=0; i<n; i++)
            for(int j=0; j<m; j++){
                dp[i][j] = 0;
                if(matrix[i][j] == '1') { dp[i][j] = 1; max= 1;}
            }
        for(int i=0; i<n; i++)
            for(int j=0; j<m; j++) {
                if(matrix[i][j] == '1' && i>0 && j>0) {
                    dp[i][j]=min(dp[i-1][j], min(dp[i-1][j-1], dp[i][j-1])) + 1;
                    if(dp[i][j] > max) max = dp[i][j]; 
                }
            }
        return max*max;
    }
```
