# [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        """
        Calculate the total amount of trapped rain water from an elevation map.
        
        Parameters:
            height (List[int]): A list of non-negative integers representing the elevation map,
                                where each integer corresponds to the height of a bar.
        
        Returns:
            int: The total amount of trapped rain water.
        """
        # If the elevation map is empty, no water can be trapped.
        if not height:
            return 0
        
        # Initialize pointers at the start and end of the list.
        left, right = 0, len(height) - 1
        
        # Variables to record the maximum height encountered from the left and right sides.
        left_max, right_max = 0, 0
        
        # This variable accumulates the total trapped water.
        trapped_water = 0
        
        # Iterate until the two pointers meet.
        while left < right:
            # If the left bar is shorter, process from the left side.
            if height[left] < height[right]:
                # Update the maximum height from the left if current height is greater.
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    # Water trapped at the current left position is the difference between the left_max and the current height.
                    trapped_water += left_max - height[left]
                left += 1  # Move the left pointer to the next position.
            else:
                # Process from the right side if the right bar is shorter.
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    # Water trapped at the current right position is the difference between the right_max and the current height.
                    trapped_water += right_max - height[right]
                right -= 1  # Move the right pointer to the previous position.
        
        return trapped_water
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** By maintaining two pointers (left and right) and updating maximum heights from both directions, the solution efficiently determines the water trapped without needing extra space for arrays, achieving an O(n) time complexity and O(1) space complexity.

- **Greedy Approach:** At each step, the decision to move the pointer with the lower height ensures that the trapped water is computed correctly, given the constraint from the side with the shorter barrier. This method avoids redundant computations.

- **Condition-Based Accumulation:** The solution uses conditional statements to update the maximum heights and accumulate trapped water. This pattern of checking and updating values can be broadly applied to scenarios such as array partitioning, sliding windows, and dynamic programming where local decisions contribute to a global optimum.