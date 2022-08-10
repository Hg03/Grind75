[Problem Statement](https://leetcode.com/problems/ransom-note/)

## Approach 1 :- In this approach, we'll create an vector of size 26(number of alphabets), then iterate the magazine and store its count in vector. Now iterate the ransomNote and if count in vector is greater than 0, decrement its count else return false(because if count is 0,element still occur means it is extra). Eventually return true.

```cpp
// Time Complexity - O(n)            Space Complexity - O(n)
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        
        
        vector<int> magazineHash(26,0);
        //Traverse magazine and keep count of each letter in magazineHash
        for(int i=0;magazine[i]!='\0';++i)
            magazineHash[magazine[i]-'a'] += 1;
        
        //Now traverse ransomNote and keep decrementing count in magazineHash
        for(int i=0;ransomNote[i]!='\0';++i)
        {
            if(magazineHash[ransomNote[i]-'a']==0)
                return false;
            magazineHash[ransomNote[i]-'a'] -= 1;   //Using up char will lead to decrementing it by value 1
        }
        return true;
    }
};
```
## Approach 2 :- Instead of using vector for storing count, we've used unordered map. Although the algorithm is same.

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        unordered_map<char,int> counts;
        for(char ch:magazine) counts[ch]++;
        for(char ch:ransomNote)
        {
            if(counts.find(ch) == counts.end()) return false;
            if(counts[ch] == 0)
                return false;
            counts[ch]--;
        }
        return true;
        
    }
};
```
