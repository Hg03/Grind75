[Problem Statement](https://leetcode.com/problems/valid-anagram/)

## Approach 1 :- In this approach, we'll iterate both string at a time and insert the value and its count in map. For string 1, increment the count and for string 2, decrement the count. This is because if both strings are anagram it means both have same number of same character. If at the end, map is empty, we'll return true else return false.

```cpp
// Time Complexity - O(n)         Space Complexity - O(n)
class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char,int> m;
        if(s.size()!=t.size()) return false;
        int n = s.size();
        for(int i=0;i<s.size();i++)
        {
            m[s[i]]++;
            m[t[i]]--;
        }
        for(auto it:m)
        {
            if(it.second) return false;
        }
        return true;
        
    }
};
```

## Approach 2 :- In this approach, we'll simply sort both strings and check their equality.

```cpp
// Time Complexity - O(nlogn)          Space Complexity - O(1)
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size()!=t.size()) return false;
        int n = s.size();
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());
        if(s == t) return true;
        return false;
    }
};
```
