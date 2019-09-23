# [Leetcode.206 Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## Question

Reverse a singly linked list.

### Example
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

## Followup
A linked list can be reversed either iteratively or recursively. Could you implement both?

## Thoughts
The iterative algorithm is pretty intuitive. Do not forget store a value that might be changed in the following step but we need to refer back to.

The recursive algorithm is more trickier. Consider how to reverse the front part, assuming the rest of the list has been reversed. Assume the list after n_k has been reversed. Then, we want n_k's next node be n_(k-1). Therefore, n_(k-1).next.next = n_(k-1). The base case is that the current node is None or the current node's next node is None. Be careful that n_1's next must point to empty.


## Solutions
### Solution.1 Iteration
```python
def reverseList(self, head: ListNode) -> ListNode:
        if head is None:
            return
        prev = None
        cur = head
        while cur is not None:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
        return prev
```

## Complex Analysis
* Time Complexity: O(N), since it just loops through the array once.
* Space Complexity: O(1), since it is a constant space solution.

### Solution.2 Recursion

```python
def reverseList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
                return head
            new_head = head.next
            head.next = None
            p = self.reverseList(new_head)
            new_head.next = head
            return p
```

## Complex Analysis
* Time Complexity: O(N), since it looks at each node once.
​

* Space Complexity: O(N). The extra space comes from implicit stack space due to recursion. The recursion could go up to n levels deep.

## Remark
* Do not forget store a value that might be changed in the following step but we need to refer back to.
* When considering recursion, we can think of induction.
