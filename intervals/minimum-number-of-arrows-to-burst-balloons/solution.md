# [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)

```python
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        """
        Determines the minimum number of vertical arrows needed to burst all balloons.
        
        Parameters:
            points (List[List[int]]): A list of intervals [x_start, x_end] representing the horizontal diameter of each balloon.
        
        Returns:
            int: The minimum number of arrows required to burst all balloons.
        """
        # Sort balloons by their ending x-coordinate.
        points.sort(key=lambda point: point[1])
        
        # Initialize the number of arrows needed and set the position of the first arrow at the end of the first interval.
        arrows = 1  # At least one arrow is needed for the first balloon.
        current_end = points[0][1]  # The x-coordinate where the first arrow is shot.
        
        # Iterate over each balloon.
        for x_start, x_end in points:
            # If the start of the current balloon is beyond the position where the last arrow was shot,
            # then the current balloon is not burst by the last arrow.
            if x_start > current_end:
                arrows += 1            # Increment arrow count as we need a new arrow.
                current_end = x_end      # Update the position for the new arrow shot at the end of the current balloon.
        
        # Return the total number of arrows required.
        return arrows
```

**Summary of Techniques and Approaches:**

- **Greedy Algorithm:** The solution uses a greedy approach by always selecting to shoot an arrow at the end of the current balloon's interval, ensuring maximum coverage of overlapping balloons. This technique optimizes for a local optimum that leads to a global optimum.

- **Sorting:** Sorting the intervals by their ending coordinate simplifies the decision-making process. Once sorted, overlapping intervals can be managed by a single arrow, which is applicable in various interval scheduling and resource allocation problems.

- **Interval Overlap Checking:** The solution checks for overlap by comparing the start of the current balloon with the end position of the previously shot arrow. This comparison strategy is widely used in problems involving intervals, merging, or scheduling.

- **Application Across Problems:** 
  - **When to Use Greedy:** Identify problems that require making a sequence of decisions where each choice is locally optimal (e.g., scheduling, interval covering, or optimization problems).
  - **Sorting as a Preprocessing Step:** Sorting based on a key characteristic (like end time for intervals) can greatly simplify problem complexity.
  - **Efficiency in Single Pass:** Iterating through sorted data in a single pass to make decisions is often efficient and reduces overhead.
  
These techniques are broadly applicable and can lead to elegant solutions in many scenarios involving optimization, scheduling, and interval processing.