# Kth Smallest Element In a Bst
Given the `root` of a binary search tree, and an integer `k`, return the `kth` smallest value **(1-indexed)** in the tree.

A **binary search tree** satisfies the following constraints:

- The left subtree of every node contains only nodes with keys **less than** the node's key.
- The right subtree of every node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees are also binary search trees.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/02eca3db-f72f-4277-7134-faec4f02e500/public)
```python
Input: root = [2,1,3], k = 1

Output: 1
```

### Example 2:

![example 2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/dca6c42d-2327-4036-f7f2-3e99d8203100/public)
```python
Input: root = [4,3,5,2,null], k = 4

Output: 5
```

### Constraints:
- 1 <= k <= The number of nodes in the tree <= 1000.
- 0 <= Node.val <= 1000

## Solution
````python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        self.k = k  # Track k as an instance variable
        self.result = None
        
        def traverse(node): # inorder traversal (ascending)
            if node is None or self.result is not None:
                return
            
            # Traverse the left subtree
            traverse(node.left)
            
            # Process the current node
            self.k -= 1
            if self.k == 0:
                self.result = node.val
                return
            
            # Traverse the right subtree
            traverse(node.right)
        
        traverse(root)
        return self.result
````