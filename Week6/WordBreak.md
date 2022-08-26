[Problem Statement](https://leetcode.com/problems/word-break)

## Approach 1 [Recursive] :- In this approach, we'll check for each character in a string and check does it belongs to our word dictionary and keep adding characters and check it recursively.

```cpp
// Time Complexity - O(len(string) * len(wordDict))         Space Complexity - O(len(string)
class Solution {
public:
    int help(int i,string s,set<string>&wordDict)
    {
        if(i==s.size()) return 1;
        string temp;
        for(int j=i;j<s.size();j++)
        {
            temp+=s[j];
            if(wordDict.find(temp)!=wordDict.end())
            {
                if(help(j+1,s,wordDict)) return 1;
            }
        }
        return 0;
    }
    bool wordBreak(string s, vector<string>& wordDict) {
        set<string> st;
        for(auto i:wordDict) st.insert(i);
        return help(0,s,st);
    }
};
```

## Approach 2 [DP] :- 

```cpp
// Time Complexity - O(n^2)             Space Complexity - O(n)
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size();
        int dp[n+1];
        memset(dp,0,sizeof(dp));
        dp[n] = 1;
        unordered_set<string> dict;
        for(string& word: wordDict)
        {
            dict.insert(word);
        }
        for(int i = n-1; i>=0;i--)
        {
            string word;            
            for(int j=i;j<n;j++)
            {
                word.push_back(s[j]);
                if(dict.find(word)!=dict.end())
                {
                    if(dp[j+1])
                        dp[i]=1;
                }
            }
        }
        return dp[0];
    }
};
```
