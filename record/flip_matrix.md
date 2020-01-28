# [1284. 转化为全零矩阵的最少反转次数](https://leetcode-cn.com/problems/minimum-number-of-flips-to-convert-binary-matrix-to-zero-matrix/)

### 题意
给你一个mxn的二进制矩阵mat。

每一步，你可以选择一个单元格并将它反转（反转表示0变1，1变0）。如果存在和它相邻的单元格，那么这些相邻的单元格也会被反转。（注：相邻的两个单元格共享同一条边。）

请你返回将矩阵 mat 转化为全零矩阵的最少反转次数，如果无法转化为全零矩阵，请返回-1 。

二进制矩阵的每一个格子要么是0要么是1。

全零矩阵是所有格子都为0的矩阵。
### 思路
1，广搜、深搜都可以
2，对于一个点，反转两次相当于没有反转。

### 代码
```cgo
private:
   static constexpr int dir[5][2]={{-1,0}, {1, 0}, {0, -1}, {0, 1}, {0, 0}};
   int Min;
public:
    int minFlips(vector<vector<int>>& mat) {
        Min= INT_MAX;
        dfs(mat, 0, 0);
        if(Min == INT_MAX) return -1;
        return Min;
    }
    
    void convert(vector<vector<int>>& mat, int pos) {
       int di = pos/mat[0].size(), dj=pos%mat[0].size();
       for(int k=0; k<5; k++) {
           int i = dir[k][0] +di;
           int j = dir[k][1] +dj;
           if(i>=0 && j>=0 && i<mat.size() && j<mat[0].size()) {
               mat[i][j] ^=1;
           }
       }
    }
    
    void dfs(vector<vector<int>>& mat, int pos, int step){
        if(pos>mat.size()*mat[0].size()) return ;// 结束条件1
        bool hasOne=false;
        for(int i=0; i<mat.size(); i++) {
            if(hasOne) break;
            for(int j=0; j<mat[0].size(); j++) {
                if(mat[i][j] == 1) {
                    hasOne = true;
                    break;
                }
            }
        }
        if(!hasOne) { // 结束条件2
            if(step < Min){
                Min = step;
                return ;
            }
        }
        convert(mat, pos);
        dfs(mat, pos+1, step+1);
        convert(mat, pos);
        dfs(mat, pos+1, step);
    }
```