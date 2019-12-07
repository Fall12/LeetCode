# [437. 路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

**思路：** 使用数组sums保存和，sums[N]代表路径上从根节点到当层节点的和。

### 主要代码
```
func pathSum(root *TreeNode, sum int) int {
    sums := make([]int64, 1003)
    sums[0] = 0
    path := 0 
    dfs(root, sum, &sums, 1, &path)
    return path
}

func dfs(root *TreeNode, sum int, sums *[]int64, cnt int, path *int)  {
	if root == nil {
		return
	}

	(*sums)[cnt] = int64(root.Val) + (*sums)[cnt-1]
	for i:=0 ; i < cnt; i++ {
		if (*sums)[cnt] - (*sums)[i] == int64(sum) {
			*path += 1
		}
	}

	dfs(root.Left, sum, sums, cnt+1, path )
	dfs(root.Right, sum, sums, cnt+1, path)
}
```