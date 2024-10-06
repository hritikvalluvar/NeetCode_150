# Binary Tree Right Side View
You are given the `root` of a binary tree. Return only the values of the nodes that are visible from the right side of the tree, ordered from top to bottom.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/d348893a-8917-456c-9599-c405cfc4e000/public)
```python
Input: root = [1,2,3]

Output: [1,3]
```
### Example 2:
```python
Input: root = [1,2,3,4,5,6,7]

Output: [1,3,7]
```

### Constraints:
- `0 <= number of nodes in the tree <= 100`
- `-100 <= Node.val <= 100`

## Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        q = deque()
        if root:
            q.append(root)

        while q:
            val = []

            for i in range(len(q)):
                node = q.popleft()
                val.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            if len(val) > 0:
                res.append(val[-1])
            
        return res
```