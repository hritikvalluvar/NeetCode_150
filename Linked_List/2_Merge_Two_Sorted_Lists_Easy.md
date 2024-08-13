# Merge Two Sorted Lists   
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one sorted linked list and return the head of the new sorted linked list.

The new list should be made up of nodes from `list1` and `list2`.

### Example 1:

![Image](/Linked_List/Images/2_Merge_Two_Sorted_Lists_Easy.avif)

```python
Input: list1 = [1,2,4], list2 = [1,3,5]

Output: [1,1,2,3,4,5]
```

### Example 2:
```python
Input: list1 = [], list2 = [1,2]

Output: [1,2]
```

### Example 3:
```python
Input: list1 = [], list2 = []

Output: []
```

### Constraints:
- `0 <= The length of the each list <= 100.`
- `-100 <= Node.val <= 100`

## Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        res = ListNode()
        curr = res
        while list1 and list2:
            if list1.val <= list2.val:
                node = ListNode(list1.val)
                curr.next = node
                list1 = list1.next
            else:
                node = ListNode(list2.val)
                curr.next = node
                list2 = list2.next
            curr = curr.next

        if list1:
            curr.next = list1
        else:
            curr.next = list2
        return res.next

        return res.next
```