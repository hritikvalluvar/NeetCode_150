# Binary Search
You are given an array of **distinct** integers `nums`, sorted in ascending order, and an integer `target`.

Implement a function to search for `target` within `nums`. If it exists, then return its index, otherwise, return `-1`.

Your solution must run in *O(logn)* time.

### Example 1:
```python
Input: nums = [-1,0,2,4,6,8], target = 4

Output: 3
```

### Example 2:
```python
Input: nums = [-1,0,2,4,6,8], target = 3

Output: -1
```

### Constraints:
- `1 <= nums.length <= 10000.`
- `-10000 < nums[i], target < 10000`

## Explanation
A binary tree is data structure which consists of a parent node which have upto 2 children nodes. The left node is smaller than the parent and the right node is greater than the parent node. To perform a binary tree search we can start from the middle, if it is smaller than the target we search the left side of the tree. If it is greater than the parent node, we search the right side of the tree. This process is repeater recursively until the target is reached, or max depth is reached.

## Solution
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        while l<=r:
            m = l + ((r - l) // 2)
            if nums[m] > target:
                r = m - 1
            elif nums[m] < target:
                l = m + 1
            else:
                return m
        return -1
```