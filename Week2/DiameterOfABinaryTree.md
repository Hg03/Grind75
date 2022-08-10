[Problem Statement](https://leetcode.com/problems/diameter-of-binary-tree)

## Approach 1 :- In this approach, recursively iterate the tree to left and right and find the diameter.

```cpp
// Time Complexity - O(n^2)          Space Complexity - O(n)
class Solution {
private:
    int height(TreeNode* node, int& diameter) {
        if (!node) {
            return 0;
        }
        int lh = height(node->left, diameter);
        int rh = height(node->right, diameter);
        diameter = max(diameter, lh + rh);
        return 1 + max(lh, rh);
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        height(root, diameter);
        return diameter;
    }
};
```

## Approach 2 :- In this approach, recursively iterate the tree and find the height of tree (updated height function)

```cpp
class Solution {
	public:
  int ans=0;

int height(TreeNode* root)
{
    if(!root) return 0;
    
    int lHeight = height(root->left);
    int rHeight = height(root->right);
    
    ans= max(ans, 1 + lHeight + rHeight);
    return 1+ max( lHeight , rHeight);

}

int diameterOfBinaryTree(TreeNode* root) {
    if(!root) return 0;
    height(root);
    return ans-1;
}

};
```

