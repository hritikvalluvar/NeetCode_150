#  Find Minimum in Rotated Sorted Array
You are given an array of length `n` which was originally sorted in ascending order. It has now been rotated between `1` and `n` times. For example, the array `nums = [1,2,3,4,5,6]` might become:

- `[3,4,5,6,1,2]` if it was rotated `4` times.
- `[1,2,3,4,5,6]` if it was rotated `6` times.

Notice that rotating the array `4` times moves the last four elements of the array to the beginning. Rotating the array `6` times produces the original array.

Assuming all elements in the rotated sorted array `nums` are unique, return the minimum element of this array.

A solution that runs in `O(n)` time is trivial, can you write an algorithm that runs in `O(log n)` time?

### Example 1:
```python
Input: nums = [3,4,5,6,1,2]

Output: 1
```
### Example 2:
```python
Input: nums = [4,5,0,1,2,3]

Output: 0
```
### Example 3:
```python
Input: nums = [4,5,6,7]

Output: 4
```
### Constraints:
- `1 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`

## Solution:
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        # if the array only has one element
        if len(nums) == 1:
            return nums[0]
            
        l, r = 0, len(nums) - 1

        # if the array is sorted
        if nums[l] < nums[r]:
            return nums[l]

        curr_min = float("inf")

        while l < r:
            mid = (l+r)//2
            curr_min = min(curr_min, nums[mid])

            # right portion has the min
            if nums[mid] > nums[r]:
                l = mid + 1
            # left portion has the min
            else:
                r = mid - 1

        return min(nums[l], curr_min)
```