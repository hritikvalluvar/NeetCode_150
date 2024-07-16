# Two Sum

Given an array of integers `nums` and an integer target, return the indices i and j such that `nums[i] + nums[j] == target` and `i != j`.

You may assume that every input has exactly one pair of indices i and j that satisfy the condition.

Return the answer with the smaller index first.

### Example 1:

```
Input: 
nums = [3,4,5,6], target = 7

Output: [0,1]
```

Explanation: nums[0] + nums[1] == 7, so we return [0, 1].

### Example 2:
```
Input: nums = [4,5,6], target = 10

Output: [0,2]
```
### Example 3:
```
Input: nums = [5,5], target = 10

Output: [0,1]
```
Constraints:
- `2 <= nums.length <= 1000`
- `-10,000,000 <= nums[i] <= 10,000,000`
- `-10,000,000 <= target <= 10,000,000`

## Solution
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = {}

        for i, num in enumerate(nums):
            compliment = target - num
            if compliment in num_to_index:
                return [num_to_index[compliment], i]
            num_to_index[num] = i
```

## Explanation
We can introduce one variable called `compliment` which is the difference between the target and the input number, and a set/hash-map `num_to_index` which can store the compliment and the index value of the corresponding input number. 

```
Input: 
nums = [3,4,5,6], target = 7

Output: [0,1]
```

1. Input number = 3
- Compliment = target - input_number = 7 - 3 = 4
- Compliment not in num_to_index
- num_to_index = {3 : 0}

2. Input number = 4
- Compliment = target - input_number = 7 - 4 = 3
- Compliment in num_to_index
- return `[0,1]`
