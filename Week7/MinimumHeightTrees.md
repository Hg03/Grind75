[Problem Statement](https://leetcode.com/problems/minimum-height-trees/)
[Solution on leetcode](https://leetcode.com/problems/minimum-height-trees/solutions/1631179/c-python-3-simple-solution-w-explanation-brute-force-2x-dfs-remove-leaves-w-bfs/?q=brute-&orderBy=most_relevant)

We are given a tree graph and we need to return array of nodes which when considered as roots form minimum heighted tree.

❌ Solution - I (Brute-Force)

We can approach this problem in brute-force manner by considering each one of the nodes as root and calculating the height of the tree thus formed. Each node which leads to minimum-height tree will be pushed in an array. If a node forms a tree with smaller height that observed till now, we will clear the array and refill if we find nodes having this smaller height. Finally this array will be returned.

To calculate height of tree formed starting at i node, we will perform a dfs traversal on all its adjacent nodes and each dfs traversal will return maximum height of tree starting at that nodes. This will be performed recursively. We will also need to maintain seen to mark node as visited so we dont keep revisiting same node again.

```cpp
class Solution {
public:
    vector<vector<int>> G;
    vector<bool> seen;
    int dfs(int i) {
        seen[i] = true;                      // mark as visited to avoid loop
        int H = 1;                           // find longest path starting from i. This gives height of tree rooted at i
        for(auto adj : G[i])
            if(!seen[adj])
                H = max(H, 1 + dfs(adj));
        seen[i] = false;                     // unmark while returning so we dont need to separately clear each element for next dfs
        return H;
    }
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& E) {
        G.resize(n); seen.resize(n);
        vector<int> ans;
        for(auto& e : E)                     // form adjacency list graph
            G[e[0]].push_back(e[1]),  
            G[e[1]].push_back(e[0]);
        
        for(int i = 0, minH = n; i < n; i++) {
            int H = dfs(i);
            if(H < minH) {                   // found smallest height till now
                minH = H;                    // update minH
                ans.clear();                 // and clear ans since all nodes in it gave larger height
            }
            if(H == minH)
                ans.push_back(i);           // push only those nodes which form minH tree
        }
        return ans;
    }
};
```

Time Complexity : O(N2), where N is the number of nodes in given tree. Each DFS takes O(N) and we make N calls in total.
Space Complexity : O(N), required for boolean array seen, stroing tree in adjacency list format in G and for recursive stack


✔️ Solution - II (2x DFS to find longest path in given graph)

This approach is based on observing the fact that there can be a maximum of 2 MHTs and the node which yields the minimum-heighted tree is(are) the mid-point(s) of longest path in the given graph.

In MHT, we want minimum distance of leaves from root node. So, it's obvious that we are trying to find a node that balances the maximum distance (height) from itself to its extreme nodes. Choosing the mid nodes of longest path (let its length be L) will ensure that the tree has its longest 2 branches, one begin of length ⌈L/2⌉ and other of ⌈L/2⌉ or ⌈L/2⌉-1 and they will differ by atmost 1 in length. Choosing any node other than the mid nodes of longest path or nodes not in longest path would off-balance the tree and lead to bigger height which would atleast be greater than ⌈L/2⌉.

Also there cant be more than 2 MHTs, 2 MHT being possible in case of even length longest path (L % 2 == 0) because there exist two mid points in this case, and 1 MHT when longest path length is odd (L%2!=0).

To find the longest path, we can choose any arbitrary node and use DFS to find the furthest node from it (call it node1). Then we can take that node and run another DFS to find furthest node from it (call it node2). We are guaranteed that node1 and node2 will be the ends of longest path. Refer this for proof. . Finally, we can return mid-point(s) of this longest path as the root nodes of MHT(s).

```cpp
class Solution {
public:
    vector<vector<int>> G;
	vector<bool> seen;
    vector<int> dfs(int i) {
		// longestPath will hold longest path found, starting from any of adjacent nodes of i
        vector<int> longestPath, path;
        seen[i] = true;                            // mark as visited to avoid loop
        for(auto adj : G[i])                       // run DFS from each adjacent node to find longest path
            if(!seen[adj]) 
                if(size(path = dfs(adj)) > size(longestPath)) 
                    longestPath = move(path);      // avoids copying...more info below
        seen[i] = false;
		longestPath.push_back(i);                  // add i itself to longest path & we get the longest path starting at i
        return longestPath;
    }
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        G.resize(n); seen.resize(n);
        for(auto& E : edges) 
            G[E[0]].push_back(E[1]), 
            G[E[1]].push_back(E[0]);
        auto path = dfs(dfs(0)[0]);                // 1st DFS from arbitrary node(0 in this case) & another DFS from furthest node returned by 1st DFS
        if(size(path) & 1)                         // 1 mid-node when path length is odd, otherwise 2
		    return {path[size(path)/2]};           
        return {path[size(path)/2], path[size(path)/2-1]};
    }
};
```

✔️ Solution - III (Remove Leaves using BFS)

Another way to find the mid-node of the tree is start from each of the leaf nodes and iteratively delete them till you are left with final 1 or 2 nodes which will be the mid-nodes.

We can find the leaf nodes at each iteration using the indegree of the node, i.e, the number of edges which are connected to the node.
A leaf node will have an indegree of 1.
The algorithm used will be similar to BFS. At each level of BFS, we will pop the leaf node and push the new nodes which become leaves after deletion of leaf nodes in the current iteration.
This will continue till we are left with only 1 or 2 nodes which would be our final mid-nodes forming the MHTs.


