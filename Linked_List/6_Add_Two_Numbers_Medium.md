# Add Two Numbers
You are given two **non-empty** linked lists, `l1` and `l2`, where each represents a non-negative integer.

The digits are stored in *reverse order*, e.g. the number 123 is represented as `3 -> 2 -> 1 ->` in the linked list.

Each of the nodes contains a single digit. You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Return the sum of the two numbers as a linked list.

### Example 1:
 
![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/fee72e19-6a21-45a5-365e-3cb45aba9700/public)

```python
Input: l1 = [1,2,3], l2 = [4,5,6]

Output: [5,7,9]

Explanation: 321 + 654 = 975.
```

### Example 2:
```python
Input: l1 = [9], l2 = [9]

Output: [8,1]
```

### Constraints:
- `1 <= l1.length, l2.length <= 100.`
- `0 <= Node.val <= 9`

## Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        head = dummy
        carry = 0

        while l1 and l2:
            total = l1.val + l2.val + carry
            unit = total % 10
            head.next = ListNode(unit)
            carry = total // 10
            head = head.next
            l1 = l1.next
            l2 = l2.next

        while carry != 0:
            if l1:
                total = l1.val + carry
                unit = total % 10
                head.next = ListNode(unit)
                carry = total // 10
                head = head.next
                l1 = l1.next
            elif l2:
                total = l2.val + carry
                unit = total % 10
                head.next = ListNode(unit)
                carry = total // 10
                head = head.next
                l2 = l2.next
            else:
                head.next = ListNode(carry)
                carry = 0
        
        if l1:
            head.next = l1
        elif l2:
            head.next = l2

        return dummy.next
```