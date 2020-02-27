#[173. 二叉搜索树迭代器](https://leetcode-cn.com/problems/binary-search-tree-iterator/)
###题意
实现一个二叉搜索树迭代器。你将使用二叉搜索树的根节点初始化迭代器。

调用next()将返回二叉搜索树中的下一个最小的数。要求O(1)时间，O(h)空间

###思路
用栈模拟中序遍历
###代码
```cgo
    BSTIterator(TreeNode* root) {
        TreeNode* p=root;
        while(p != NULL){
            s.push(p);
            p=p->left;
        }
    }
    
    /** @return the next smallest number */
    int next() {
        TreeNode* x=s.top();
        s.pop();
        TreeNode* temp = x;
        if(temp->right!= NULL) {
            s.push(temp->right);
            temp=temp->right;
            while(temp->left!= NULL) {
                s.push(temp->left);
                temp=temp->left;
            }
        }
        return x->val;
    }
```