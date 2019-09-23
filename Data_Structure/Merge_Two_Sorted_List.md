# [Leetcode.206 Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

## Question

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

### Example
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```



## Thoughts
For iterative algorithm, we set up a false "`prehead`" node that allows us to easily return the head of the merged list later. We also maintain a `new` pointer, which points to the current node for which we are considering adjusting its `next` pointer. Then, we do the following until at least one of `l1` and `l2` points to `None`: if the value at `l1` is less than or equal to the value at `l2`, then we connect `l1` to the previous node and increment `l1`. Otherwise, we do the same, but for `l2`. Then, regardless of which list we connected, we increment `new` to keep it one step behind one of our list heads.

After the loop terminates, at most one of `l1` and `l2` is non-`Nonw`. Therefore (because the input lists were in sorted order), if either list is non-`None`, it contains only elements greater than all of the previously-merged elements. This means that we can simply connect the non-`None` list to the merged list and return it.


For recursive algorithm, we model the above recurrence directly, first accounting for edge cases. Specifically, if either of `l1` or `l2` is initially `None`, there is no merge to perform, so we simply return the non-`None` list. Otherwise, we determine which of `l1` and `l2` has a smaller head, and recursively set the next value for that head to the next merge result. Given that both lists are `None`-terminated, the recursion will eventually terminate.


## Solutions
### Solution.1 Iteration
```python
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        prehead = ListNode(-1)
        new = prehead
        while l1 is not None and l2 is not None:
                if l1.val > l2.val:
                    new.next = l2
                    l2 = l2.next
                    new = new.next
                else:
                    new.next = l1
                    l1 = l1.next
                    new = new.next
        if l1 is not None:      
            new.next = l1
        if l2 is not None:
            new.next = l2
        return prehead.next

```

## Complex Analysis
* Time Complexity: O(N+M). Because exactly one of `l1` and `l2` is incremented on each loop iteration, the `while` loop runs for a number of iterations equal to the sum of the lengths of the two lists.
* Space Complexity: O(1), since it is a constant space solution.

### Solution.2 Recursion

```python
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
  if l1 is None:
        return l2
    if l2 is None:
        return l1
    if l1.val > l2.val:
        l2.next = self.mergeTwoLists(l1, l2.next)
        return l2
    else:
        l1.next = self.mergeTwoLists(l1.next, l2)
        return l1
```

## Complex Analysis
* Time Complexity: O(N+M), since there will be exactly one call to `mergeTwoLists` per element in each list.
​

* Space Complexity: O(N+M). The first call to `mergeTwoLists` does not return until the ends of both l1 and l2 have been reached, so n+m stack frames consume O(n + m)O(n+m) space.

## Remark
* Creating prehead trick
* Combining two loops together to decrease the time complexity
* Do not need to create a new list. Just connect nodes in existing lists.
