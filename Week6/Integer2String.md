[Problem Statement](https://leetcode.com/problems/integer-to-english-words/)

## Approach :- 

```cpp
class Solution {
public:
    string numberToWords(int num) {
        if(!num)
            return "Zero";
        
        string ones[] = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
        string tens[] = {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
        string elevens[] = {"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
        
        int count = 0;
        string ans;
        int flag;
        while(num > 0)
        {
            count++;
            string temp;
            int prev;
            
            flag = 0;
            for(int j = 1; num > 0 && j <= 3; j++)
            {
                int x = num%10;
                num = num/10;
                
                if(j == 2)
                {
                    if(x == 1) // to check if in eleven series
                        temp = " "+elevens[prev];
                    else if(x) // to check if in tens series
                        temp = " "+tens[x]+temp;                        
                }                    
                else if(j == 3)
                {
                    if(x)
                        temp = " " + ones[x] + " Hundred" + temp;                        
                }                   
                else if(x)
                    temp = " "+ones[x];
                // to check if there any non zero number in entire 3 digit number, so to correspondingly add thousand, million in next stage
                if(x) 
                    flag = 1;
                
                prev = x;
            }
            
            if(count == 2)
            {
                if(flag)
                    ans = temp + " Thousand" + ans;
            }                
            else if(count == 3)
            {
                if(flag)
                    ans = temp + " Million" + ans;
            }                
            else if(count == 4)
                    ans = temp + " Billion" + ans;               
            else
                ans = temp;
        }       
     
        //removing initial whitespaces if any
        string whitespaces (" ");
        int start = ans.find_first_not_of(whitespaces);
        if (start!=string::npos)
        ans.erase(0,start);
        
        return ans;
    }
    
    
};
```
