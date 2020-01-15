# [279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

### 题意
给定正整数n，找到若干个完全平方数（比如1,4,9,16,...）使得它们的和等于n。你需要让组成和的完全平方数的个数最少。

示例 1:

输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.

### 思路
动态规划

### 代码
```cgo
    int numSquares(int n) {
      vector<int> dp(n+1);
      dp[1] = 1;
      for(int i=2; i<=n; i++) {
          int minN = i;
          for(int j=1;j*j<=i;j++) {
              int index=i-j*j;
              int newMin = dp[index]+1;
              if(newMin<minN) minN= newMin;  
          }
          dp[i] = minN;
      }  
      return dp[n];
    }
```

### 广搜代码
尽量往0走，每次将新得到的差值入队列
```cgo
class Node{
public:
    int data, step;
    Node(int, int);
};
Node::Node(int d, int s): data(d), step(s){};

class Solution {
public:
    int numSquares(int n) {
        queue<Node*> q;
        Node *node = new Node(n, 0);
        q.push(node);
        vector<int> visit(n+1, 0);
        while(!q.empty()) {
            Node *node = q.front();
            q.pop();

            for(int i=1;i*i<=node->data;i++) {
                int newData= node->data-i*i;
                if(newData == 0) return node->step+1;
                if(!visit[newData]){
                    q.push(new Node(newData, node->step+1));
                    visit[newData] = 1;
                }
            }
        }
        return n;
    }
};
```