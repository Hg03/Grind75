[Problem Statement](https://leetcode.com/problems/course-schedule/)

## Approach [Graph] :- In this approach, we simply has to check the cycle in graph ,if cycle exist return false that it is impossible to finish the courses.

We are creating a directed graph with help of this array (in form of adjacency list) like 
                                             
![alt image](https://github.com/Hg03/Grind75/blob/main/imgs/courseschedule.png)


Clearly, in this approach, we'll create a map of courses with its prerequisites. Now iterate each course with its prerequisites until the prerequisites of each course is not empty. If courses(act as key and prerequisites as a value) list become empty means course can be finished. Parallely when visiting courses ,insert it in set ,if something repeated, means course can't be finished.
                                             

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
        unordered_set<int> visited;  // to store each course only one time, if course occurs one more time, it can't be finished
        
        for (int course = 0; course < numCourses; course++) {    // Iterate the courses using depth first search
            if (!dfs(course, m, visited)) {
                return false;
            }
        }
        return true;
    }
private:
    bool dfs(int course, unordered_map<int, vector<int>>& m, unordered_set<int>& visited) {
        if (visited.find(course) != visited.end()) {   // If course comes more than 1 times
            return false;
        }
        if (m[course].empty()) {                      // If course's prerequisites becomes empty, we can finish the course
            return true;
        }
        visited.insert(course);
        for (int i = 0; i < m[course].size(); i++) {   // Iterate the next courses
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
