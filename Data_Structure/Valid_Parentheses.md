# [Leetcode.20 Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

## Question

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

### Example 1
```
Input: "()"
Output: true
```

### Example 2
```
Input: "()[]{}"
Output: true
```

### Example 3
```
Input: "(]"
Output: false
```

### Example 4
```
Input: "([)]"
Output: false
```

### Example 5
```
Input: "{[]}"
Output: true
```

## Thoughts
Use Stack. This question is easy.

## Solutions
### Solution.1 Brute force
```python
def isValid(self, s: str) -> bool:
        stack = [ ]
        mapping = {")": "(", "}": "{", "]": "["}

        for char in s:
            if char in mapping:
                if stack == []:
                    return False
                top_element = stack.pop()
                if mapping[char] != top_element:
                    return False
            else:
                stack.append(char)

        return not stack
```

## Complex Analysis
* Time Complexity: O(N). We traverse the list containing N elements. `append()` and `pop()` take linear time.

* Space Complexity: O(N), as we push all opening brackets onto the stack and in the worst case, we will end up pushing all the brackets onto the stack. e.g. `((((((((((`

## Remark
* Debug carefully before submitting.
* When have a question about matching, consider the use of dictionary.
