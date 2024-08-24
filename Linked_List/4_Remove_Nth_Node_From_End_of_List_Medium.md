# Remove Nth Node From End of List
You are given the beginning of a linked list `head`, and an integer `n`.

Remove the `nth` node from the end of the list and return the beginning of the list.

### Example 1:
```python
Input: head = [1,2,3,4], n = 2

Output: [1,2,4]
```

### Example 2:
```python
Input: head = [5], n = 1

Output: []
```

### Example 3:
```python
Input: head = [1,2], n = 2

Output: [2]
```

### Constraints:
- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

## Explanation
`Nth` position from the end can also be expressed as `(m-n)th` position from the start given `m` is the length of the linked list. `m` can be calculated out in `O(n)` time. Finding the node to be removed can be traversed in `O(m-n)` time. After reaching the previous node of the desired node, the next link can be upadted as the next node of the desired node. So the total time complexity is `O(n) + O(m-n)`.

## Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        left = dummy
        right = head
        while n > 0:
                right = right.next
                n -= 1

        while right:
            left = left.next
            right = right.next
        
        left.next = left.next.next

        return dummy.next
```