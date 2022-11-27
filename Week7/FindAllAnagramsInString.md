[Problem Statement](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Approach 1 :- Finding all substrings of size (p) and cheacking if it is anagram or not.

```cpp
// TLEd
class Solution {
public:
    bool areAnagram(string str1, string str2)
    {
        sort(str1.begin(), str1.end());
        for (int i=0;i<str1.size();i++)
        {
            if (str1[i]!=str2[i])
            {
                return false;
            }
        }
        return true;
    }
    vector<int> findAnagrams(string s, string p) {
        vector<string> v;
        vector<int> ans;
        string k="";
        for(int i=0;i<s.size();i++)
        {
            for(int j=i;j<i+p.size() && j<s.size();j++)
            {
                k+=s[j];
            }
            if(k.size()==p.size())
            {
                v.push_back(k);   
            }
            k="";
        }
        sort(p.begin(),p.end());
        for(int i=0;i<v.size();i++)
        {
            if(areAnagram(v[i],p))
            {
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```
## Approach 2 :- Optimized 1

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        int s_len = s.length();
        int p_len = p.length();
        
        if(s.size() < p.size()) return {};
        
        vector<int> freq_p(26,0);
        vector<int> window(26,0);
        
        //first window
        for(int i=0;i<p_len;i++){
            freq_p[p[i]-'a']++;
            window[s[i]-'a']++;
        }
        
        vector<int> ans;
        if(freq_p == window) ans.push_back(0);
        
        for(int i=p_len;i<s_len;i++){
            window[s[i-p_len] - 'a']--;
            window[s[i] - 'a']++;
            
            if(freq_p == window) ans.push_back(i-p_len+1);
        }
        return ans;
    }
    
};
```


## Approach 3 :- Using hash table

```cpp
 class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> ans;
        vector<int> hash(26, 0);
        vector<int> phash(26, 0);
        int window = p.size();
        int len = s.size();
        if(len < window)
        {
            return ans;
        }
        int left = 0,right = 0;
        while(right < window)
        {
            phash[p[right] - 'a'] += 1;
            hash[s[right] - 'a'] += 1;
            right++;
        }
        right -=1;
        while(right < len)
        {
            if(phash == hash)
            {
                ans.push_back(left);
            }
            right+=1;
            if(right != len)
            {
                hash[s[right] - 'a'] += 1;
            }
            hash[s[left] - 'a'] -=1 ;
            left += 1;
        }
        return ans;
    }
};
```
[Refer This](https://leetcode.com/problems/find-all-anagrams-in-a-string/solutions/1739169/c-sliding-window-hash-table-intuitive/)
