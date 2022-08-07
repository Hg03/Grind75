[Problem Statement](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

## Approach :- In this approach, traverse the tree by following some conditions :
- if root is equal to p or q , return root.
- if p present in left subtree and q present in right subtree ,return root.
- if p and q both present in left or right subtree, simply traverse recursively.
- if not p nor q found in any portion, return null.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL) return NULL;
        if(root == p || root == q) return root;
        TreeNode* leftT = lowestCommonAncestor(root->left,p,q);
        TreeNode* rightT = lowestCommonAncestor(root->right,p,q);
        if(leftT == NULL) return rightT;
        if(rightT == NULL) return leftT;
        return root;
    }
};
```
[If confuse refer it](https://youtu.be/cOjLyASDJcc)
