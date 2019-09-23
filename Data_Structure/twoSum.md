# [Leetcode.1 Two Sum](https://leetcode.com/problems/two-sum/)

## Question

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## Thoughts
The brute force solution requires two loops, which costs so much time. After coming up with this brute force solution, we need to consider hash map or two pointers, which might save more time.

## Solutions
### Solution.1 Brute force
```python
def BruteForcetwoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return None
```

## Complex Analysis
* Time Complexity: O(n^2), since we run a loop inside another.
* Space Complexity: O(1), since it is a constant time solution.

### Solution.2 Hashmap

```python
def twoSum(self, nums, target):
  complementMap = { }
  for i in range(len(nums)):
    num = nums[i]
    complement = target - num
    if complement in complementMap:
      j = complementMap[complement]
      return [i, j]
    complementMap[num] = i
```

## Complex Analysis
* Time Complexity: O(n). We traverse the list containing nn elements only once. Each look up in the table costs only O(1) time.

* Space Complexity: O(n). The extra space required depends on the number of items stored in the hash table, which stores at most n elements.
