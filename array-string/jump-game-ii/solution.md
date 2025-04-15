# [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/description/)

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        """
        Compute the minimum number of jumps to reach the last index in the array.
        
        Parameters:
            nums (List[int]): A list of non-negative integers where each element represents 
                              the maximum jump length from that index.
        
        Returns:
            int: The minimum number of jumps needed to reach the last index.
        """
        n = len(nums)
        # If there's only one element, you're already at the end.
        if n <= 1:
            return 0
        
        jumps = 0         # Counter for the number of jumps made so far.
        current_end = 0   # The farthest index reachable within the current jump.
        farthest = 0      # The farthest index reachable from all indices considered in the current jump.
        
        # Traverse through the array; no need to check the last element.
        for i in range(n - 1):
            # Update the farthest reachable index from index i.
            farthest = max(farthest, i + nums[i])
            
            # When we've reached the end of the current jump, it's time to jump.
            if i == current_end:
                jumps += 1              # Increment the jump counter.
                current_end = farthest  # Set the new jump's boundary as the farthest index found.
                
                # If this new boundary reaches or exceeds the last index, exit early.
                if current_end >= n - 1:
                    break
        
        return jumps
```

**Summary of Techniques and Approaches:**

- **Greedy Algorithm:** This solution greedily selects the farthest reachable index from the current interval, ensuring that each jump covers the maximum possible distance. This idea of "greedily" expanding the reach is applicable to many optimization problems.

- **Two-Pointer/Interval Tracking:** By maintaining two pointers—one for the current boundary (`current_end`) and one for the furthest reachable index (`farthest`)—we dynamically update our jump boundaries. This technique can be used in problems involving intervals or ranges.

- **Single-Pass Iteration:** The algorithm iterates over the list once (O(n) time complexity). Look for opportunities to solve problems using a single traversal to optimize performance.

- **Early Termination:** The loop exits as soon as the current jump range reaches the last index, demonstrating a technique to avoid unnecessary computation in scenarios where a condition is met early.

These strategies are broadly applicable to various problems involving optimization, dynamic range updates, and greedy selections.