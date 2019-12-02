# [124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/submissions/)

**注意点：**

1. 需要在递归的过程，比对子树的和是否比最大值大
2. 如果子树的值小于0，那么直接设置为0

**代码：**

	var maxSum int
	func max(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	func maxPathSum(root *TreeNode) int {
		maxSum = root.Val
		dfs(root)
		return maxSum
	}
	
	func dfs(root *TreeNode) int {
		if root == nil {
			return 0
		}
		leftSum := max(0, dfs(root.Left))
		rightSum := max(0, dfs(root.Right))
		maxSum = max(maxSum, leftSum+rightSum+root.Val) // 比对左根右的这种情况
		return max(leftSum, rightSum) + root.Val // 返回的是较大的左右子树
	}
  
