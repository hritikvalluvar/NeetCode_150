# Longest Consecutive Sequence
Given an array of integers `nums`, return the length of the longest consecutive sequence of elements.

A consecutive sequence is a sequence of elements in which each element is exactly 1 greater than the previous element.

You must write an algorithm that runs in O(n) time.

### Example 1:
```python
Input: nums = [2,20,4,10,3,4,5]

Output: 4
```
Explanation: The longest consecutive sequence is [2, 3, 4, 5].

Example 2:
```python
Input: nums = [0,3,2,5,4,6,1,1]

Output: 7
```
Constraints:
- `0 <= nums.length <= 1000`
- `-10^9 <= nums[i] <= 10^9`

## Solution
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0

        numSet = set(nums)
        longest = 0

        for n in numSet:
            if (n - 1) not in numSet:
                length = 1
                while (n + length) in  numSet:
                    length += 1
                longest = max(longest, length)
        
        return longest
```

## Explanation
A set data type is used to store only the unique elements of `nums` called `numSet`. The set is traversed one by one and if the element does not have any prior element in `numSet`, the posterior elements are checked in `numSet`. If posterior exists, the `length` variable of the sequence is updated. And if it is longer than the `longest` variable which stores the length of the longest sequence, `longest` is updated. 