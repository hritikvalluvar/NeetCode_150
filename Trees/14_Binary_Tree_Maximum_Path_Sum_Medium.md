# Binary Tree Maximum Path Sum
Given the `root` of a *non-empty* binary tree, return the maximum **path sum** of any *non-empty* path.

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes has an edge connecting them. A node can not appear in the sequence more than once. The path does not necessarily need to include the root.

The path sum of a path is the sum of the node's values in the path.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/9896b041-9021-44c2-ab3e-5cff76adf100/public)

```python
Input: root = [1,2,3]

Output: 6
```

Explanation: The path is 2 -> 1 -> 3 with a sum of 2 + 1 + 3 = 6.

### Example 2:

![example 2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/19ce1187-387e-4323-f2c9-1a317ab36200/public)

```python
Input: root = [-15,10,20,null,null,15,5,-5]

Output: 40
```

Explanation: The path is 15 -> 20 -> 5 with a sum of 15 + 20 + 5 = 40.

### Constraints:
- `1 <= The number of nodes in the tree <= 1000.`
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
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = [root.val]
        def dfs(root):
            if not root:
                return 0
            leftMax = dfs(root.left) 
            rightMax = dfs(root.right)
            leftMax = max(leftMax, 0)
            rightMax = max(rightMax, 0)

            res[0] = max(res[0], root.val + leftMax + rightMax)
            return root.val + max(leftMax, rightMax)

        dfs(root)
        return res[0]
```
