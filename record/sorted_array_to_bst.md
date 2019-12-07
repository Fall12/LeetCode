# [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

### 题意
将有序数组转换为二叉搜索树，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

### 思路
数组有序，二分法

### 代码
```
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        int size = nums.size();
        if(size<=0) {
            return NULL;
        }
        int mid = (0 + size) >> 1;
        TreeNode* root = new TreeNode(nums.at(mid));
        binary(root, nums, 0, mid-1, true);
        binary(root, nums, mid+1, size-1, false);
        return root;
    }
    void binary(TreeNode* root, vector<int> &nums, int left, int right, bool isLeft) {
        if (left > right) {
            return;
        }
        int mid = (left + right ) >> 1;
        TreeNode* node = new TreeNode(nums.at(mid));
        if (isLeft == true) {
           root->left = node; 
        } else {
            root->right = node;
        }
        binary(node, nums, left, mid-1, true);
        binary(node, nums, mid+1, right, false);
    }
};

```