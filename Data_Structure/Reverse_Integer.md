# [Leetcode.7 Reverse Linked List](https://leetcode.com/problems/reverse-integer/)

## Question

Given a 32-bit signed integer, reverse digits of an integer.

### Example1
```
Input: 123
Output: 321
```
### Example2
```
Input: -123
Output: -321

```
### Example3
```
Input: 120
Output: 21
```


## Note
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Thoughts
We can reverse each digit or do it mathematically.

## Solutions
### Solution.1 Math
```python
class Solution:
    def reverse(self, x: int) -> int:
        rev = 0
        neg = False
        if x < 0:
            neg = True
            x = -1 * x
        while x >= 1:
            a = x%10
            x = x//10
            rev = rev*10 + a
            if rev > 2**31 - 1 or rev < (-2)**31:
                return 0
        if neg is True:
            return -1*rev
        return rev
```

## Complex Analysis
* Time Complexity: O(N), since it just loops through the array once.
* Space Complexity: O(1), since it is a constant space solution.

### Solution.2 Digit

```python
class Solution:
    def reverse(self, x: int) -> int:
        s = str(abs(x))

        rev = int(s[::-1])

        if rev > 2**31 - 1:
            return 0

        return rev if x > 0 else (-1*rev)
```

## Complex Analysis
* Time Complexity: O(N), since it just loops through the array once.
* Space Complexity: O(1), since it is a constant space solution.
