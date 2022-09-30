[Problem Statement](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

## Approach 1 :- In this approach, find the path of given node from root node for both given node. Then iterate the list of paths of both nodes and return the recent common node which lowest common ancestor.

```cpp
class Solution {
public:
     void rootToNode(TreeNode* root, TreeNode* target, vector<TreeNode*>& path, bool& found){
        // If tree is empty
        if(!root)return;        
        
        // Push the root node
        path.push_back(root);
         
        // If root is our target node
        if(root->val == target->val){
            found = true;
            return;
        }
        
        // Search further for target node
        if(!found)rootToNode(root->left, target, path, found);        
        if(!found)rootToNode(root->right, target, path, found);
         
        // If we didn't get the node's value, we'll pop the root node also from list
        if(!found){
            path.pop_back(); 
            return;
        }
    }
    
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root)return root;
        
        vector<TreeNode*> Path_for_p;
        bool found = false;
        // Finding path for p from root node
        rootToNode(root, p, Path_for_p, found);
        
        vector<TreeNode*> Path_for_q;
        found = false;
        // Finding path for q from root node
        rootToNode(root, q, Path_for_q, found);
        

        TreeNode* lca = new TreeNode();
        int i = 0;
        // Checking the last common node that is eventually the lowest ancestor
        while(i<Path_for_p.size() && i<Path_for_q.size()){
            if(Path_for_p[i] != Path_for_q[i])break;
            lca = Path_for_p[i];
            i++;
        }
        return lca;
    }
};
```
## Approach 2 :- In this approach, traverse the tree by following some conditions :
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
