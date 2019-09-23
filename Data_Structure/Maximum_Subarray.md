# [Leetcode.53 Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

## Question

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Example
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Followup
If you have figured out the O(N) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## Thoughts
In greedy algorithm, we can use two variables to store maximum sum so far and current sum. In each iteration, we first update current sum by taking the bigger one of current value and it plus previous current sum. Then, update maximum sum according to it.

In divide and conquer algorithm, we can divide the array in the middle and use recursion to calculate the maximum subarray of each of these two until we get the base case where subarray only contains one element. Besides calculating right sum and left sum, we have to consider the case where maximum subarray cross the right subarray and left subarray. In this case, we calculate maximum subarray starting from the middle point going to either right or left and finally sum them together. Finally, the recursion should return the largest among right, left, and cross.


## Solutions
### Solution.1 Greedy Algorithm
```python
def maxSubArray(self, nums: List[int]) -> int:
        maxSum = nums[0]
        curSum = nums[0]

        for i in range(1, len(nums)):
            curSum = max(nums[i], curSum + nums[i])
            maxSum = max(maxSum, curSum)
        return maxSum
```

## Complex Analysis
* Time Complexity: O(N), since it just loops through the array once.
* Space Complexity: O(1), since it is a constant space solution.

### Solution.2 Divide and conquer

```python
def maxSubArray(self, nums: List[int]) -> int:
        return self.recSum(nums, 0, len(nums)-1)

    def recSum(self, nums, left, right):
        if left == right:
            return nums[left]
        p = (left+right)//2

        leftSum = self.recSum(nums, left, p)
        rightSum = self.recSum(nums, p+1, right)
        crossSum = self.crossSum(nums, left, right, p)
        return max(leftSum, rightSum, crossSum)

    def crossSum(self, nums, left, right, p):
        if left == right:
            return nums[left]

        leftSum = float('-inf')
        curSum = 0
        for i in range(p, left-1, -1):
            curSum = curSum + nums[i]
            leftSum = max(leftSum, curSum)

        rightSum = float('-inf')
        curSum = 0
        for i in range(p+1, right+1):
            curSum = curSum + nums[i]
            rightSum = max(rightSum, curSum)

        return leftSum + rightSum
```

## Complex Analysis
* Time Complexity: O(NlogN). According to master theorem, T(N) = aT(N/b)+theta(N^d). Here one divides the problem in two subproblemes `a = 2`, the size of each subproblem (to compute left and right subtree) is a half of initial problem `b = 2`, and all this happens in a O(N) time `d = 1`. That means `log_b(a)=d=1`. Therefore, the time complexity is O(N^(log_b(a))N) = O(NlogN).
​

* Space Complexity: O(logN), to keep recursion stack.

## Remark
* Consider all corner cases!
* Two pointer trick is helpful!
* Divide and Conquer basically uses recursion to divide the problem into subproblems. We need define the base case and consider cases when combining two subproblems together!
