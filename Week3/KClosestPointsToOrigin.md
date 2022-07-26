[Problem Statement](https://leetcode.com/problems/k-closest-points-to-origin/)

## Approach 1 :- In this approach, we'll create a vector of pair of pair. We'll iterate all the points and calculate the distance, then store the distance with its coordinates.After iteration, we'll sort the vector then iterate that vector and print its first k values.

```cpp
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        vector<pair<int,pair<int,int>>> v;
        vector<vector<int>> ans;
        int dist,x,y;
        for(int i=0;i<points.size();i++)
        {
            x = points[i][0];
            y = points[i][1];
            dist = pow(x,2) + pow(y,2);
            v.push_back({dist,{x,y}});
        }
        sort(v.begin(),v.end());
        for(int i=0;i<k;i++)
        {
            ans[i].push_back(v[i].second.first);
            ans[i].push_back(v[i].second.second);
        }
        return ans;
        
    }
};
```


**Whenever question includes find kth maximum, minimum, smallest and largest, max or min heap is the optimised solution**

**When we create priority queue in c++, bydefault it act as a maxHeap(means when we pop, it returns us the largest)**

**If you require minHeap, make the elements negative while pushing, and when using top or printing it ,make it positive again**

## Approach 2 [MaxHeap] :- In this approach, we'll use max heap using priority queue of vector(2D). We'll push the distance with its x and y coordinates upto k limit. If limit k exceeds, We'll pop from priority queue. Finally our queue contains minimum element. So just pop k element's coordinates.

```cpp
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
         //Answer vector
        vector<vector<int>> result(k);
        //maxheap storage initialization
        priority_queue<vector<int>> maxHeap;
        //Construction of maxheap
        for (auto& p : points) {
            int x = p[0], y = p[1];
            maxHeap.push({x*x + y*y, x, y});
            if (maxHeap.size() > k) {
                maxHeap.pop();
            }
        }
        
        for (int i = 0; i < k; ++i) {
            vector<int> top = maxHeap.top();
            maxHeap.pop();
            result[i] = {top[1], top[2]};
        }
        
        return result;
    }
};
```
[Learn more about priority queues](https://youtu.be/yAs3tONaf3s)
