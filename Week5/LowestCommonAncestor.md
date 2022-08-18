[Problem Statement](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## Approach :- In this we simply need to find the subtree's root which will contain both p and q, right?! So we do the same,

1. Well, if there is no root, you gotta return null/root. if(root==nullptr) { return root; }
2. if your root contains either p or q, you return that root. WHY?? because it will be used in calculation of two different answer A.K.A. left and right side of tree.

3. Now save your Left answer of the left side of tree in a variable, this variable with either have a null or a valid node depending on recursive calls if it finds the required node, Do the same for the Right side make a variable and save the answer.

4. Now, we have two different variables namely left and right. Both contains answer either null or a valid node, now we check three conditions.

- If Left answer is not null and right answer is also not null, then the answer is the root itself, since left and right are subtrees of the root and if both are not null it clearly means p and q lies in right as well as left side,

- If left answer is not null but right answer is null, then it means both p and q lies on the left side of tree inside the subtree with root as left answer, return left answer.

- If right answer is not null but left answer is null, then it means both p and q lies on the right side of tree inside the subtree with root as right answer, return right answer.

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) 
    {
        if(root== NULL)
        {
            return NULL;
        }
        if(root== p || root== q)
        {
            return root;
        }
        TreeNode* left= lowestCommonAncestor(root->left, p, q);
        TreeNode* right= lowestCommonAncestor(root->right, p, q);
        if(left!= NULL && right!= NULL)
        {
            return root;
        }
        else if(left!= NULL)
        {
            return left;
        }
        else if(right!= NULL)
        {
            return right;
        }
        return NULL;
    }
};
```
