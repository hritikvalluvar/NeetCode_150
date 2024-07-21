# Products of Array Except Self
Given an integer array `nums`, return an array `output` where `output[i]` is the product of all the elements of `nums` except `nums[i]`.

Each product is **guaranteed** to fit in a **32-bit** integer.

Follow-up: Could you solve it in *O(n)* time without using the division operation?

### Example 1:
```python
Input: nums = [1,2,4,6]

Output: [48,24,12,8]
```
### Example 2:
```python
Input: nums = [-1,0,1,2,3]

Output: [0,-6,0,0,0]
```

### Constraints:
- `2 <= nums.length <= 1000`
- `-20 <= nums[i] <= 20`

## Solution
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = []
        prefix  = 1
        postfix = 1

        for i in range(len(nums)):
            res.append(prefix)
            prefix = prefix * nums[i]

        for i in range(len(nums) - 1, -1, -1):
            res[i] = res[i] * postfix
            postfix = postfix * nums[i]
        
        return res
```

## Explanation
![image](/Arrays_and_Hashing/Images/prod_except_self.jpeg)

### 1st Pass(Prefix)

The prefix is initialized as `prefix=1` since there is no prefix of the first element. In each iteration:

- The prefix is appended to the result array. 
- The prefix is updated by multiplying the current element to the prefix.

For example, for the 3rd element which is 3, the product of prefix is 2. It is saved in the 3rd element of the result array.

### 2nd Pass(Postfix)
The postfix is initialized as `postfix=1` since there is no postfix of the last element. In each iteration:

- The `res[i]` is updated by multiplying the postfix with the `res[i]`.
- The postfix is updated by multiplying `res[i]` to itself.
