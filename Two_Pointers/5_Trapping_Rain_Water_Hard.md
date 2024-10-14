# Trapping Rain Water
You are given an array non-negative integers `heights` which represent an elevation map. Each value `heights[i]` represents the height of a bar, which has a width of `1`.

Return the maximum area of water that can be trapped between the bars.

### Example 1:

![example 1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/0c25cb81-1095-4382-fff2-6ef77c1fd100/public)

```
Input: height = [0,2,0,3,1,0,1,3,2,1]

Output: 9
```

### Constraints:
- `1 <= height.length <= 1000`
- `0 <= height[i] <= 1000`

## Solution
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if len(height) < 3:
            return 0
        l ,r = 0, len(height) - 1

        maxL, maxR = height[l], height[r]
        result = 0

        while l < r:
            if maxR > maxL:
                l += 1
                maxL = max(maxL, height[l])
                result += maxL - height[l]
            else:
                r -= 1
                maxR = max(maxR, height[r])
                result += maxR - height[r]
        return result
```