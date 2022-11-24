[Problem Statement](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

# Approach 1 [Brute Force] :- 

```cpp
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        vector<string> answer;
        
        if (digits.size() == 0) {
            return answer;
        }
        
        answer.push_back("");

        vector<string> mapping = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        for (auto number: digits) {
            string &letters = mapping[number - '2'];
            
            // Fix the vector size
            // "a", "b", "c" -> "a", "b", "c", "a", "b", "c", "a", "b", "c"
            int sz = answer.size();
            for (int i = 1; i < letters.size(); ++i) {
                for (int j = 0; j < sz; ++j)
                    answer.push_back(answer[j]);
            }
            
            // Append the current number's letters to all the existing strings
            // "a", "b", "c", "a", "b", "c", "a", "b", "c" ->
            // "ad", "bd", "cd", "ae", "be", "ce", "af", "bf", "cf"
            int pos = 0;
            for (int i = 0; i < letters.size(); ++i)
                for (int j = 0; j < answer.size()/letters.size(); ++j)
                    answer[pos++].push_back(letters[i]);
        }
        return answer;
    }
};
```

# Approach 2 :- Backtracking

```cpp
// Time Complexity - O(4^N * N)           Space Complexity - O(N)
class Solution {
  public:
    vector < string > letterCombinations(string digits) {
      if (!digits.size()) {
        return {};
      }
 
      vector < string > combs;
      const vector < string > chars = {
        "0",
        "1",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
      };
      string builder;
      build(builder, 0, digits, chars, combs);
      return combs;
    }
  void build(string builder, int i,
    const string & digits,
      const vector < string > & chars, vector < string > & combs) {
    if (i == digits.size()) {
      combs.push_back(builder);
      return;
    }
 
    int d = digits[i] - '0';
    for (char ch: chars[d]) {
      build(builder + ch, i + 1, digits, chars, combs);
    }
  }
};
```

