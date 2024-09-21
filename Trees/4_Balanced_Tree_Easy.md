# Balanced Tree
Given a binary tree, return `true` if it is height-balanced and `false` otherwise.

A **height-balanced** binary tree is defined as a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

### Example 1:

![example 2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/c19c3727-ea28-416c-3873-79ee75f2b400/public)

```python
Input: root = [1,2,3,null,null,4]

Output: true
```

### Example 2:

![example 2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/24fcc2da-e012-4f9e-856e-040f200f3c00/public)

```python
Input: root = [1,2,3,null,null,4,null,5]

Output: false
```
### Example 3:
```python
Input: root = []

Output: true
```

### Constraints:
- The number of nodes in the tree is in the range `[0, 1000].`
- `-1000 <= Node.val <= 1000`

## Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]
            
            left, right = dfs(root.left), dfs(root.right)
            balanced = ( left[0] and right[0] and ( abs(left[1] - right[1]) <= 1 ) )
            return [balanced, 1 + max(left[1], right[1])]
        return dfs(root)[0]
```