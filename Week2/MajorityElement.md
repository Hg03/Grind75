[Problem Statement](https://leetcode.com/majority-element/)

## Approach 1 :- In this approach, we'll iterate array and check each number and its count, then if it's count is greater than majority count, return number else -1.

```cpp
// Time Complexity - O(n^2)            Space Complexity - O(1)
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int majorityCount = nums.size()/2;
        for(int num : nums)
        {
            int count = 0;
            for(int elem : nums)
            {
                if(elem == num)
                    count++;
            }
            if(count > majorityCount)
                return num;
        }
        return -1;
    }
};
```

## Approach 2 :- In this approach, we'll use hasmap to store elements and its count. Then we'll iterate the map and check which element has count greater than majority count.

```cpp
Time Complexity - O(NlogN)      Space Complexity - O(N)
class Solution {
public:
    int majorityElement(vector<int>& nums) {
       
       unordered_map<int,int> m;
       for(int i=0;i<nums.size();i++) m[nums[i]]++;
       for(auto i:m)
       {
           if(i.second > nums.size()/2) return i.first;
       }
       return 0;
        
        
    }
};
```

## Approach 3 [Moore Voting algorithm] :- This algorithm works on the fact that if an element occurs more than N/2 times, it means that the remaining elements other than this would definitely be less than N/2. So let us check the proceeding of the algorithm. First, choose a candidate from the given set of elements if it is the same as the candidate element, increase the votes. Otherwise, decrease the votes if votes become 0, select another new element as the new candidate.

```cpp
// Time Complexity - O(n)         Space Complexity - O(1)
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        // Moore voting algorithm
        int votes = 0;
        int candidate = 0;
        for(int num : nums)
        {
            if(votes == 0) candidate = num;
            if(num == candidate) votes++;
            else votes--;
        }
        return candidate;
    }
};
```
