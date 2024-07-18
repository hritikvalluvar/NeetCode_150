# Top K Frequent Elements
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements within the array.

The test cases are generated such that the answer is always unique.

You may return the output in any order.

### Example 1:
```
Input: nums = [1,2,2,3,3,3], k = 2

Output: [2,3]
```
### Example 2:
```
Input: nums = [7,7], k = 1

Output: [7]
```

### Constraints:

- `1 <= nums.length <= 10^4.`
- `-1000 <= nums[i] <= 1000`
- `1 <= k <= number of distinct elements in nums.`

## Solution
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        freq = [[] for i in range(len(nums) + 1)]

        for n in nums:
            count[n] = 1 + count.get(n, 0)

        for n, c in count.items():
            freq[c].append(n)

        res = []
        for i in range(len(nums), 0, -1):
            for n in freq[i]:
                res.append(n)
                if len(res)==k:
                    return res
```

## Explanation
```python
nums = [6,7,7,7,8,8,8,8,8]
k = 2
```

- `count` is a hash map which saves the count of the elements, where the elements are the key and the count are the values. 

```python
count = {6: 1, 7: 3, 8: 5}
```

- `freq` is a nested array which saves where the count is the index and the elements are the values. 

```python
#     |-0----1---2----3---4----5---6---7---9---10-|
freq = [[], [6], [], [7], [], [8], [], [], [], []]
```

- `res` is the result array which iterates from right to left and is returned when length of `res` is equal to `k`  

`res = [8, 7]`