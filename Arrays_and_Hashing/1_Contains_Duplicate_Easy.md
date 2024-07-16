# Contains Duplicate

Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

### Example 1:

```
Input: nums = [1, 2, 3, 3]

Output: true
```

### Example 2:

```
Input: nums = [1, 2, 3, 4]

Output: false
```

## Solution

```python
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        return len(nums) != len(set(nums))
```

## Explanation
Set in python stores only unique values. So if the length of the array and the set of the same array are same it can be deduced that the array only contains unique value.