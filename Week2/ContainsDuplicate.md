[Problem Statement](https://leetcode.com/problems/contains-duplicate/)

## Approach 1 :- In this approach, we'll create a map and store the element and its count, then we iterate the map check if any element's count is greater than 1. We'll return that element.

```cpp
// Time Complexity - O(n)             Space Complexity - O(n)
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_map<int,int> m;
        for(auto a:nums) m[a]++;
        for(auto a:m){
            if(a.second > 1) return true;
        }
        return false;
    }
};
```

## Approach 2 :- In this approach, we'll use set in which we store element of array and if that element already exist in set, it means that one is the duplicate.

```cpp
// Time Complexity - O(n)             Space Complexity - O(n)
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> s;
        for(auto i:nums) s.insert(i);
        if(nums.size()==s.size()) return false;
        return true;
        
    }
};
```

## Approach 3 :- Sort the array and check the consecutive elements ,if they are equal means they are duplicate.

```cpp
// Time Complexity - O(nlogn)             Space Complexity - O(1)
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(),nums.end());
        for(int i=0;i<n-1;i++){
            if(nums[i] == nums[i+1]) return true;
        }
        return false;
        
    }
};
```
