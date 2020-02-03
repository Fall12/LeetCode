# [60. 第k个排列](https://leetcode-cn.com/problems/permutation-sequence/)

###题意
给出集合 [1,2,3,…,n]，其所有元素共有n!种排列。

按大小顺序列出所有排列情况，并一一标记，当n=3时, 所有排列如下：
"123"
"132"
"213"
"231"
"312"
"321"
给定n和k，返回第k个排列。
### 思路
递归分组
### 代码
```cgo
    void group( int k, int n, int number, vector<int> &visited) {
        if(number <= 0 )  return ;
        int per = 1;
        for(int i=1; i<number; i++) per *=i;
        int newIndex = k/per;
        if(k%per != 0) newIndex +=1;
        int newK = k- (newIndex-1)*per;
        for(int i=1; i<=n ;i++)
            if(!visited[i]) {
                newIndex --;
                if(newIndex == 0) {
                    newIndex = i;
                    break;
                }
            }
        visited[newIndex] = 1;
        s += newIndex + '0';
        group(newK, n, number-1, visited);
    }
    string getPermutation(int n, int k) {
        if(n == 1) return "1";
        vector<int> visited(n+1, 0);
        s = "";
        group(k, n, n, visited);
        return s;
    }
```