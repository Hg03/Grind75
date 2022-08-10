[Problem Statement](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

## Approach 1 :- In this approach, we'll calculate the left and right height recursively and eventually calculate the max between left and right height plus 1.

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        int left = maxDepth(root->left);
        int right =maxDepth(root->right);
        return 1 + max(left,right);
    }
};
```
