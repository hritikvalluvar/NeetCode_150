# Median of Two Sorted Arrays 
You are given two integer arrays `nums1` and `nums2` of size `m` and `n` respectively, where each is sorted in ascending order. Return the median value among all elements of the two arrays.

Your solution must run in *O(log(m+n))* time.

### Example 1:
```python
Input: nums1 = [1,2], nums2 = [3]

Output: 2.0
```

Explanation: Among `[1, 2, 3]` the median is 2.

### Example 2:
```python
Input: nums1 = [1,3], nums2 = [2,4]

Output: 2.5
```
Explanation: Among `[1, 2, 3, 4]` the median is (2 + 3) / 2 = 2.5.

### Constraints:
- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `-10^6 <= nums1[i], nums2[i] <= 10^6`

## Solution
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        A, B = nums1, nums2

        if len(B) < len(A):
            A, B = B, A
        
        total   = len(A + B)
        half    = total // 2
        l, r    = 0, len(A) - 1

        while True:
            i = (l+r) // 2
            j = half - i - 2

            Aleft   = A[i]      if i >= 0           else float("-inf")
            Aright  = A[i+1]    if (i+1) < len(A)   else float("inf")
            Bleft   = B[j]      if j >= 0           else float("-inf")
            Bright  = B[j+1]    if (j+1) < len(B)   else float("inf")

            if Aleft <= Bright and Bleft <= Aright:
                if total % 2:
                    return min(Aright, Bright)
                else:
                    return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
            elif Aleft > Bright:
                r = i - 1
            else:
                l = i + 1
```