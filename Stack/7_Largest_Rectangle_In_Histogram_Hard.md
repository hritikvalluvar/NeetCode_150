# Largest Rectangle In Histogram
You are given an array of integers `heights` where `heights[i]` represents the height of a bar. The width of each bar is `1`.

Return the area of the largest rectangle that can be formed among the bars.

### Example 1:
![example 1](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)
```python
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```
### Example 2:
```python
Input: heights = [1,3,7]

Output: 7
```
### Constraints:
- `1 <= heights.length <= 1000.`
- `0 <= heights[i] <= 1000`

## Solution
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        maxArea = 0
        stack = []

        for i, h in enumerate(heights):
            start = i
            while stack and stack[-1][1] > h:
                index, height = stack.pop()
                maxArea = max(maxArea, height * (i - index))
                start = index
            stack.append((start, h))
        
        for i, h in stack:
            maxArea = max(maxArea, h * (len(heights) - i))

        return maxArea
```