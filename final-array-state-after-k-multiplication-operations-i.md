# 3264. Final Array State After K Multiplication Operations I

https://leetcode.com/problems/final-array-state-after-k-multiplication-operations-i/description/

# Intuition

Use a priority queue / heap to keep track of the current minumum value in the array.

# Approach

Build a heap using Python's `heapq` module. Populate it with (`value`, `index`) pairs based on the original list.
Now we do the following steps `k` times.

1. Pop the smallest value from the heap.
2. Update the pair by multiplying the value by `multiplier`
3. Push the updated pair back onto the heap.
4. Also update the original `nums` list with the updated value.

Note that `heappop(my_heap)` and `heappush(my_heap, item)` maintain a valid heap by automatically reheaping.

# Complexity

- Time complexity:
  $$O(n*log(n))$$

- Space complexity:
  $$O(n)$$

# Code (Python)

```
import heapq
class Solution:
    def getFinalState(self, nums: List[int], k: int, multiplier: int) -> List[int]:
        heap = [(nums[i], i) for i in range(len(nums))]
        heapq.heapify(heap)
        for _ in range(k):
            min_pair = heapq.heappop(heap)
            min_pair = (min_pair[0]*multiplier, min_pair[1])
            heapq.heappush(heap, min_pair)
            nums[min_pair[1]] = min_pair[0]
        return nums
```
