# Lowest Common Ancestor of a Binary Search Tree
Given a binary search tree (BST) where all node values are *unique*, and two nodes from the tree `p` and `q`, return the lowest common ancestor (LCA) of the two nodes.

The lowest common ancestor between two nodes `p` and `q` is the lowest node in a tree `T` such that both `p` and `q` as descendants. The ancestor is allowed to be a descendant of itself.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/2080ee6a-3d27-4cd5-0db2-07672ead8200/public)
```python
Input: root = [5,3,8,1,4,7,9,null,2], p = 3, q = 8

Output: 5
```

### Example 2:

![example 2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/2080ee6a-3d27-4cd5-0db2-07672ead8200/public)
```python
Input: root = [5,3,8,1,4,7,9,null,2], p = 3, q = 4

Output: 3
```

Explanation: The LCA of nodes 3 and 4 is 3, since a node can be a descendant of itself.


### Constraints:
- `2 <= The number of nodes in the tree <= 100.`
- `-100 <= Node.val <= 100`
- `p != q`
- `p` and `q` will both exist in the BST.

## Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        while True:
            if root.val < p.val and root.val < q.val:
                root = root.right
            elif p.val < root.val and q.val < root.val:
                root = root.left
            else:
                return root

```