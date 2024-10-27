# Last Stone Weight
You are given an array of integers `stones` where `stones[i]` represents the weight of the `ith` stone.

We want to run a simulation on the stones as follows:

- At each step we choose the **two heaviest stones**, with weight `x` and `y` and smash them together.
- If `x == y`, both stones are destroyed
- If `x < y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

Continue the simulation until there is no more than one stone remaining.

Return the weight of the last remaining stone or return `0` if none remain.

### Example 1:

```python
Input: stones = [2,3,6,2,4]

Output: 1
```

Explanation:
We smash 6 and 4 and are left with a 2, so the array becomes [2,3,2,2].
We smash 3 and 2 and are left with a 1, so the array becomes [1,2,2].
We smash 2 and 2, so the array becomes [1].

### Example 2:

```python
Input: stones = [1,2]

Output: 1
```

### Constraints:
- `1 <= stones.length <= 20`
- `1 <= stones[i] <= 100`

## Solution

```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # stones = [2,3,6,2,4]
        flipped = [-num for num in stones] # [-2, -3, -6, -2, -4]
        heapq.heapify(flipped) # [-6, -4, -2, -2, -3]

        while len(flipped) > 1:
            largest, secondLargest = heapq.heappop(flipped), heapq.heappop(flipped) # largest = -6, secondLargest = -4 

            if largest < secondLargest: # -6 < -4
                diff = secondLargest - largest # diff = -4 - (-6) = 2
                heapq.heappush(flipped, - diff) # push -2

        return - flipped[0] if len(flipped) > 0 else 0 # return -1
```