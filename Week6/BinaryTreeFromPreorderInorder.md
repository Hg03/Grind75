[Problem Statement](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)

## Approach :- In this , we know that in preorder array, first element is root of binary tree, then next is root of left subtree and next is root left's left subtree and when left ends, root of right subtree's value appear and so on.
When we choose root with the help of preorder array, we search that element in inorder, from inorder we depict ,array of elements left to it is the part of left subtree and its right to it is the part of right subtree and so on.

```cpp
// Time Complexity - O(N)            Space Complexity - O(N)
class Solution {
public:
        TreeNode * buildTree(vector < int > & preorder, int preStart, int preEnd, vector < int > & inorder, int inStart, int inEnd, map < int, int > & mp) {
      if (preStart > preEnd || inStart > inEnd) return NULL;

      TreeNode * root = new TreeNode(preorder[preStart]);
      int elem = mp[root -> val];
      int nElem = elem - inStart;

      root -> left = buildTree(preorder, preStart + 1, preStart + nElem, inorder,
      inStart, elem - 1, mp);
      root -> right = buildTree(preorder, preStart + nElem + 1, preEnd, inorder, 
      elem + 1, inEnd, mp);

      return root;
    }

    TreeNode * buildTree(vector < int > & preorder, vector < int > & inorder) {
      int preStart = 0, preEnd = preorder.size() - 1;
      int inStart = 0, inEnd = inorder.size() - 1;

      map < int, int > mp;
      for (int i = inStart; i <= inEnd; i++) {
        mp[inorder[i]] = i;
      }

      return buildTree(preorder, preStart, preEnd, inorder, inStart, inEnd, mp);
    }
};
```
