# [264. 丑数 II](https://leetcode-cn.com/problems/ugly-number-ii/)
### 题意
编写一个程序，找出第n丑数。

丑数就是只包含质因数2,3,5的正整数，1也是丑数。

### 思路
分组计算，将相等的都往后移动

### 代码
```cgo
    int min(int a, int b) {
        if(a<b) return a;
        return b;
    }
    int nthUglyNumber(int n) {
        vector<int> ans(n);
        ans[0] = 1;
        int index2=0,index3=0,index5=0;
        for(int i=1;i<n;i++) {
            int val =min(ans[index2]*2, min(ans[index3]*3, ans[index5]*5));
            ans[i] = val;
            if(ans[index2]*2 == val) index2++;
            if(ans[index3]*3 == val) index3++;
            if(ans[index5]*5 == val) index5++;
        }
        return ans[n-1];
    }
```

# [313. 超级丑数](https://leetcode-cn.com/problems/super-ugly-number/)
### 题意
输入: n=12,primes=[2,7,13,19]  
输出: 32   
解释: 给定长度为4的质数列表primes=[2,7,13,19]，前12个超级丑数序列为：[1,2,4,7,8,13,14,16,19,26,28,32] 。

### 思路
类似上题，分组计算
### 代码
```cgo
    int nthSuperUglyNumber(int n, vector<int>& primes) {
                vector<int> dp(n+1, 0);
        dp[0]=1;
        vector<int> index(primes.size(), 0);

        for(int i=1; i<n; i++) {
            int Min= INT_MAX;
            for(int j=0; j<primes.size(); j++) {
                long data = primes[j]* dp[index[j]];
                if(data<Min) {
                    Min = data;
                }
            }
            for(int j=0; j<primes.size(); j++) {
                if(primes[j] *dp[index[j]] == Min) {
                    index[j]++;
                }
            }
            dp[i] = Min;
        }
        for(int i=0; i<n; i++) cout<<dp[i]<< " ";
        return dp[n-1];
    }
```
 