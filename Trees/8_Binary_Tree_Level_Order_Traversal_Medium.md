# Binary Tree Level Order Traversal 
Given a binary tree `root`, return the level order traversal of it as a nested list, where each sublist contains the values of nodes at a particular level in the tree, from left to right.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/a4639809-0754-4eda-221f-a4cd58bd9c00/public)
```python
Input: root = [1,2,3,4,5,6,7]

Output: [[1],[2,3],[4,5,6,7]]
```

### Example 2:
```python
Input: root = [1]

Output: [[1]]
```
### Example 3:
```python
Input: root = []

Output: []
```

### Constraints:
- `0 <= The number of nodes in both trees <= 1000.`
- `-1000 <= Node.val <= 1000`

## Solution
```python
from collections import deque
from typing import Optional, List

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        q   = deque(root) # deque for storing all the nodes of a level
        if root:
            q.append(root) # initialise deque with root

        while q:
            level = [] # Stores all values of a single level

            for i in range(len(q)):
                node = q.popleft()
                if node:
                    level.append(node.val)
                    if node.left:
                        q.append(node.left)
                    if node.right:
                        q.append(node.right)
            res.append(level)
        return res
```