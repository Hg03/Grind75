[Problem Statement](https://leetcode.com/problems/course-schedule/)

## Approach [Graph] :- In this approach, we simply has to check the cycle in graph ,if cycle exist return false that it is impossible to finish the courses.

We are creating a directed graph with help of this array (in form of adjacency list) like 
                                             
![alt image](https://github.com/Hg03/Grind75/blob/main/imgs/courseschedule.png)
                                             

```cpp
// Time Complexity(as well as Space) - O(v + e) where v is the vertex(values) and edges are connections
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        // map each course to prereq list
        unordered_map<int, vector<int>> m;
        for (int i = 0; i < prerequisites.size(); i++) {
            m[prerequisites[i][0]].push_back(prerequisites[i][1]);
        }
        // all courses along current DFS path
        unordered_set<int> visited;
        
        for (int course = 0; course < numCourses; course++) {
            if (!dfs(course, m, visited)) {
                return false;
            }
        }
        return true;
    }
private:
    bool dfs(int course, unordered_map<int, vector<int>>& m, unordered_set<int>& visited) {
        if (visited.find(course) != visited.end()) {
            return false;
        }
        if (m[course].empty()) {
            return true;
        }
        visited.insert(course);
        for (int i = 0; i < m[course].size(); i++) {
            int nextCourse = m[course][i];
            if (!dfs(nextCourse, m, visited)) {
                return false;
            }
        }
        m[course].clear();
        visited.erase(course);
        return true;
    }
};
```
