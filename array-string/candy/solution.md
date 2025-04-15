# [135. Candy](https://leetcode.com/problems/candy/description/)

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        """
        Distribute candies to children based on ratings, ensuring:
        - Each child gets at least one candy.
        - Children with higher ratings than a neighbor receive more candies.
        
        Parameters:
            ratings (List[int]): List of integers representing each child's rating.
            
        Returns:
            int: The minimum number of candies required for distribution.
        """
        n = len(ratings)
        # Initialize the candies list with 1 candy for each child.
        candies = [1] * n
        
        # First pass: left-to-right.
        # If the current child has a higher rating than the previous child,
        # increment the candy count from the previous child.
        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                candies[i] = candies[i - 1] + 1
        
        # Second pass: right-to-left.
        # If the current child has a higher rating than the next child,
        # ensure the current child's candies count is one more than the next child's.
        # Use max to preserve the maximum from the left-to-right pass.
        for i in range(n - 2, -1, -1):
            if ratings[i] > ratings[i + 1]:
                candies[i] = max(candies[i], candies[i + 1] + 1)
        
        # Sum of all candies is the answer.
        return sum(candies)
```

**Summary of Techniques and Approaches:**

- **Two-Pass Strategy:** 
  - **Left-to-Right Pass:** Guarantees that each child with a higher rating than the previous one gets one more candy.
  - **Right-to-Left Pass:** Reinforces this condition in reverse, ensuring that children with higher ratings than their right neighbor get at least one more candy than that neighbor.
- **In-Place Updates with Auxiliary Array:** Maintaining an auxiliary array (here, `candies`) to store the computed candy counts simplifies the implementation and helps in combining the information from both passes.
- **Utilization of `max`:** When performing the right-to-left pass, using the `max` function ensures that the requirement imposed by the left-to-right pass is not overridden.
- **General Application Tips:**
  - Use multi-pass algorithms when conditions are directional (e.g., dependencies on neighbors).
  - Break the problem into manageable passes that address different constraints.
  - Ensure consistency by merging the results from each pass carefully, often with simple functions like `max` or `min`.
  
These techniques are broadly applicable in problems involving dynamic programming, greedy algorithms, or constraints based on neighboring elements.