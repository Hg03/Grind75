[Problem Statement](https://leetcode.com/evaluate-reverse-polish-notation/)

## Approach :- In this approach, we'll use stack and follow the below procedure.
- If operand appears, push it in stack.
- If operator appears, pop 2 elements from stack ,then apply the operation and push the result it in stack.

```cpp
// Time Complexit - O(n)           Space Complexity - O()
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
	stack<int> s;
	for(auto& t : tokens) 
		if(t == "+" || t == "-" || t == "*" || t == "/") {
			int op1 = s.top(); s.pop();
			int op2 = s.top(); s.pop();
			if(t == "+") op1 = op2 + op1;
			if(t == "-") op1 = op2 - op1;
			if(t == "/") op1 = op2 / op1;
			if(t == "*") op1 = op2 * op1;   
			s.push(op1);
		}
		else s.push(stoi(t));    // stoi - converts from string to int     
	return s.top(); 
    }
};
```
