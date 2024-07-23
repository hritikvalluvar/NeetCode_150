# Container With Most Water
You are given an integer array `heights` where `heights[i]` represents the height of the i<sup>th</sup>  bar.

You may choose any two bars to form a container. Return the maximum amount of water a container can store.

### Example 1:
![image](/Two_Pointers/Images/max_depth.avif)
```python
Input: height = [1,7,2,5,4,7,3,6]

Output: 36
```

### Example 2:
```python
Input: height = [2,2,2]

Output: 4
```
### Constraints:
- `2 <= height.length <= 1000`
- `0 <= height[i] <= 1000`

## Solution
```python
class Solution:
    def maxArea(self, heights: List[int]) -> int:
        deepest = 0
        l, r = 0, len(heights) - 1

        while l < r:
            depth = min(heights[l], heights[r]) * (r - l)
            deepest = max(depth, deepest)

            if heights[l] < heights[r]:
                l += 1
            else:
                r -= 1

        return deepest
```