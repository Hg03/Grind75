[Problem Statement](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)

## Approach 1 :- In this approach, we'll iterate element and its next element to check its difference with tracking of maximum value.

```cpp
// Time Complexity - O(n^2)      Space Complexity - O(1)
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxProfit = 0;
        for(int i=0;i<prices.size()-1;i++)
        {
            for(int j=i+1;j<prices.size();j++)
            {
                maxProfit = max(maxProfit,prices[j]-prices[i]);
            }
        }
        return maxProfit;
    }
};
```

## Approach2 :- In this approach, we'll keep track of minimum from start and check the next values and find the max profit.

```cpp
// Time Complexity - O(n)          Space Complexity - O(1)
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxPro = 0;
        for(int i = 0;i<prices.size();i++){
            minPrice = min(minPrice,prices[i]);
            maxPro = max(maxPro,prices[i] - minPrice);
        }
        return maxPro;
    }
};
```
