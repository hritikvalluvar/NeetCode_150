# 3Sum
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` where` nums[i] + nums[j] + nums[k] == 0`, and the indices `i`, `j` and `k` are all distinct.

The output should not contain any duplicate triplets. You may return the output and the triplets in any order.

### Example 1:
```python
Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]
```

Explanation:

`nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.`

`nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.`

`nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.`

The distinct triplets are `[-1,0,1]` and `[-1,-1,2]`.

### Example 2:
```python
Input: nums = [0,1,1]

Output: []
```
Explanation: The only possible triplet does not sum up to 0.

### Example 3:
```python
Input: nums = [0,0,0]

Output: [[0,0,0]]
```
Explanation: The only possible triplet sums up to 0.

### Constraints:
- `3 <= nums.length <= 1000`
- `-10^5 <= nums[i] <= 10^5`

## Solution
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for i in range(len(nums) - 2):
            l, r = i + 1, len(nums) - 1
            if nums[i] > 0: # If the smallest element is greater than 0 there is no possible solution.
                break
            if i > 0 and nums[i] == nums[i - 1]: # Skipping lowest redudant elements
                continue
            while l < r:
                curSum = nums[i] + nums[l] + nums[r]

                if curSum == 0:
                    res.append([nums[i], nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while nums[l] == nums[l - 1] and l < r: # Skipping redudant elements
                                l += 1
                elif curSum > 0:
                    r -= 1
                else:
                    l += 1
        return res
```