# [55. Jump Game](https://leetcode.com/problems/jump-game/description/)

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        """
        Determine whether the last index of the list 'nums' can be reached from the first index.
        
        Each element in 'nums' represents the maximum jump length from that position.
        The function returns True if the end of the list is reachable, otherwise False.
        
        Parameters:
            nums (List[int]): A list of non-negative integers representing maximum jump lengths.
        
        Returns:
            bool: True if the last index is reachable, otherwise False.
        """
        farthest = 0  # This variable tracks the farthest index we can reach so far.
        n = len(nums)  # Total number of positions in the list.
        
        # Iterate through each index in the array.
        for i in range(n):
            # If the current index is greater than the farthest reachable index,
            # it means we are stuck and cannot progress further.
            if i > farthest:
                return False
            
            # Update the farthest reachable index from the current position.
            farthest = max(farthest, i + nums[i])
            
            # If we've already reached or passed the last index, return True.
            if farthest >= n - 1:
                return True
        
        # If the loop completes, check whether the last index was reached.
        return False
```

**Summary of Techniques and Approaches:**

- **Greedy Algorithm:** The solution employs a greedy strategy by tracking the farthest reachable index while iterating through the array. In each step, the algorithm updates the current reach based on the current element and uses early termination to detect if the destination is reachable. This approach has a time complexity of O(n), making it highly efficient for large datasets.

- **Single-Pass Iteration:** Iterating through the list once ensures that the algorithm checks all necessary positions without redundant work. The early exit condition (when the farthest reachable index meets or exceeds the last index) is a key optimization.

- **In-Place Updating:** The technique leverages the input array without requiring additional data structures, aligning with principles for in-place computation and space efficiency.

- **Broad Applicability:** This greedy method can be adapted to solve various problems involving range reachability, interval expansion, or decision-making under constraints. Recognizing when to use a greedy approach generally comes from identifying that a local optimal choice (the farthest jump at each step) leads to a global solution.

- **Tip for Other Problems:** When faced with problems that require making a sequence of choices (like jumping over elements or processing intervals), analyze if maintaining and updating a single representative variable (like the farthest reachable index) can simplify the problem and lead to an optimal solution without exhaustive search.