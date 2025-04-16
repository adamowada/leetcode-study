# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        """
        Calculate the maximum area of water that can be contained by two vertical lines.
        
        Parameters:
            height (List[int]): A list of integers representing the heights of vertical lines.
            
        Returns:
            int: The maximum area of water that the container can store.
        """
        left = 0                        # Left pointer starting at the beginning of the list.
        right = len(height) - 1         # Right pointer starting at the end of the list.
        max_area = 0                    # Variable to store the maximum area found.
        
        # Loop until the two pointers meet.
        while left < right:
            current_width = right - left           # Distance between the two pointers.
            current_height = min(height[left], height[right])  # Height limited by the shorter line.
            current_area = current_width * current_height      # Area formed by the two lines.
            
            # Update the maximum area if the current area is larger.
            max_area = max(max_area, current_area)
            
            # Move the pointer corresponding to the shorter line inward,
            # since this is the limiting factor for the container's height.
            if height[left] < height[right]:
                left += 1        # Increase left pointer to try for a taller line.
            else:
                right -= 1       # Decrease right pointer to try for a taller line.
                
        return max_area
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** By initializing pointers at both ends and moving the pointer at the shorter line inward, the algorithm efficiently explores the solution space in linear time. This approach reduces the problem's time complexity from O(n²) to O(n).

- **Greedy Strategy:** The choice of moving the pointer at the smaller height is a greedy decision aimed at increasing the potential area in future iterations.

- **In-Place Calculation:** No extra space is used aside from a few variables, making it both space efficient and easy to understand.

**General Tips:**

- Use the two-pointer technique in array problems where the solution involves finding pairs that optimize a condition, especially when the array is sorted or can be processed from both ends.
- Identify the limiting factor in the problem (like the shorter vertical line in this problem) to decide which pointer to move.
- Focus on in-place modifications and greedy decisions to reduce unnecessary computations and optimize the overall efficiency of your solution.