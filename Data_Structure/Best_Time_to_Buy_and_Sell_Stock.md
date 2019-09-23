# [Leetcode.7 Reverse Linked List](https://leetcode.com/problems/reverse-integer/)

## Question

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.
### Example1
```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```
### Example2
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

```

## Thoughts
`Max profit` always comes after `Min price`. Therefore, just keep track of the lowest price. Update `Max profit` when `current price - Min price` is greater than it.

## Solutions
### Solution.1 Brute Force
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max_p = 0
        for i in range(len(prices)):
            cur = prices[i]
            for j in range(i+1, len(prices)):
                if prices[j]-cur > max_p:
                    max_p = prices[j]-cur
        return max_p

```

## Complex Analysis
* Time Complexity: O(N^2), since it runs n(n-1)/2 times.
* Space Complexity: O(1), since it is a constant space solution.

### Solution.2 One pass

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_p = float('inf')
        max_profit = 0
        for p in prices:
            if p < min_p:
                min_p = p
            elif p - min_p > max_profit:
                max_profit = p - min_p
        return max_profit
```

## Complex Analysis
* Time Complexity: O(N), since it just loops through the array once.
* Space Complexity: O(1), since it is a constant space solution.

## Remark
* Use examples to help you think.
* Sometimes drawing a graph can help.
