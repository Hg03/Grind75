[Problem Statement](https://leetcode.com/problems/binary-tree-right-side-view)

## Approach :- In this approach, we'll perform reverse preorder traversal (Root -> Right -> Left), in which we have 2 base conditions i.e.
- if root == null, return
- if size of vector in which we are storing the result == level of tree ,push root->val in vector (means here if we encounter the level first time and that is also the rigth view of particular level)
- Iterate recursively to right and then left.

```cpp
// Time Complexity - O(n)              Space Complexity - O(height of a tree)
class Solution {
public:
    void findRightView(TreeNode* root,int level,vector<int>& res)
    {
        if(root == NULL) return;
        if(res.size() == level) res.push_back(root->val);
        findRightView(root->right,level+1,res);
        findRightView(root->left,level+1,res);
    }
    vector<int> rightSideView(TreeNode* root) {
        vector<int> res;
        findRightView(root,0,res);
        return res;
    }
};
```
