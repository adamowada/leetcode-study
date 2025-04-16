# [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        """
        Finds two numbers in a sorted list 'numbers' that add up to 'target' and returns their 1-indexed positions.
        
        Parameters:
            numbers (List[int]): A list of integers sorted in non-decreasing order.
            target (int): The target sum to achieve with two numbers from 'numbers'.
        
        Returns:
            List[int]: A list containing the 1-indexed positions of the two numbers that add up to target.
        """
        left, right = 0, len(numbers) - 1  # Initialize two pointers at the beginning and end of the list.
        
        # Loop until the two pointers meet
        while left < right:
            current_sum = numbers[left] + numbers[right]  # Sum of the numbers at the two pointers.
            
            # Check if the current sum equals the target
            if current_sum == target:
                # Return 1-indexed positions
                return [left + 1, right + 1]
            
            # If the sum is less than target, move the left pointer to the right to increase the sum.
            elif current_sum < target:
                left += 1
            
            # If the sum is greater than target, move the right pointer to the left to decrease the sum.
            else:
                right -= 1

        # Given the problem constraints, there is always exactly one solution.
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** Leveraging the sorted nature of the input array allows you to efficiently search for the correct pair by initializing two pointers at opposite ends and moving them inward. This pattern is particularly useful when the array is sorted.

- **In-place Operation with Constant Space:** The solution doesn't require additional data structures, making it optimal in terms of space usage. This is a key consideration when a problem stipulates constant extra space.

- **Iterative Approach:** Using a single-pass iteration ensures an O(n) time complexity, a strategy that can be applied in any problem where one traversal of the array is sufficient to capture the necessary information.

- **General Problem-Solving Insight:** When the input data exhibits a certain order or pattern (like a sorted array), it is often beneficial to tailor a solution that exploits that structure, reducing complexity and enhancing performance. This approach can be extended to problems involving finding pairs or triplets that satisfy a condition.