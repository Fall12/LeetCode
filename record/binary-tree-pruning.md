# [814. 二叉树剪枝](https://leetcode-cn.com/problems/binary-tree-pruning/)

### 题意
给定二叉树根结点root，此外树的每个结点的值要么是0，要么是1。
返回移除了所有不包含1的子树的原二叉树。
(节点X的子树为X本身，以及所有X的后代。)

### 代码
```cgo
class Solution {
public:
    TreeNode* pruneTree(TreeNode* root) {
        if(root == NULL) {
            return NULL;
        }
        root->left = pruneTree(root->left);
        root->right = pruneTree(root->right);
        if(root->left == NULL && root->right == NULL && root->val == 0) {
            return NULL;
        }
        return root;
    }
};

```