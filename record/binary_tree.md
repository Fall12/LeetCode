# 二叉树相关

## [113. 路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

#### 题意 
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。【输出路径】

说明: 叶子节点是指没有子节点的节点。

**注意：** 
1. 注意空树的判断
2. 回溯算法
3. 结果的保存需要注意 

```
func pathSum(root *TreeNode, sum int) [][]int {
    var res [][]int 
    if root == nil {
        return res
    }
    stack := make([]int, 1000) 
    cnt := 0
    currentSum := 0
    dfs(root, stack, cnt, currentSum, sum, &res)
    return res 
}
	
func dfs(root *TreeNode, stack []int, cnt int, currentSum, sum int, res *[][]int) {
    if root == nil {
        return 
    }
	
    if root.Val + currentSum == sum {
        if root.Left == nil && root.Right == nil {
            ans := make([]int, cnt+1 )
            for i :=0; i< cnt; i++ {
                ans[i] = stack[i]
            }
            ans[cnt] = root.Val
            *res = append(*res, ans)
            return 
        }
    }
	
    stack[cnt] = root.Val
    dfs(root.Left, stack, cnt+1, currentSum+root.Val, sum, res)
    dfs(root.Right, stack, cnt+1, currentSum+root.Val, sum, res)
}
```
### [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)

**注意**  叶子节点是指没有子节点的节点。

```
func hasPathSum(root *TreeNode, sum int) bool {
    if root == nil  {
        return false
    }
    
    res := false 
    dfs(root, 0, sum, &res)
    return res 
}
func dfs(root *TreeNode, currentSum, sum int, res *bool) bool {
    if *res {
        return true 
    }
    if root == nil {
        if currentSum != sum {
            return false 
        }
        return true 
    }
    
    left := dfs(root.Left, currentSum+root.Val, sum, res)
    right := dfs(root.Right, currentSum + root.Val, sum, res)
    
    if left && right {
        *res = true 
        return true
    }
    return false  
}
```