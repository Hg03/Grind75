[Problem Statement](https://leetcode.com/problems/first-bad-version)

## Approach 1 :- In this approach, we'll traverse the version linearly, and everytime asks that it is bad or not. (It takes lot of api calls)

## Approach 2 [Binary Search] :- In this approach, we'll search the element and ask the api(badVersion) that it is bad or not. If it is not bad it means we are somewhere at the starting point, so we should go the right side i.e. shift your left to mid+1 or else if it is bad, shift to mid.

```cpp
// Time Complexity - O(logn)           Space Complexity - O(1)
class Solution {
public:
    int firstBadVersion(int n) {
        int lower = 1, upper = n, mid;
        while(lower < upper) {
            mid = lower + (upper - lower) / 2;
            if(!isBadVersion(mid)) lower = mid + 1;   /* Only one call to API */
            else upper = mid;
        }
        return lower;   /* Because there will alway be a bad version, return lower here */
    }
};
```
