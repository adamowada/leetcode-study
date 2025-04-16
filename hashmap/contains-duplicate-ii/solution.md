# [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/)

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        """
        Determine if the array 'nums' contains two distinct indices i and j such that
        nums[i] == nums[j] and the absolute difference between i and j is at most k.
        
        Parameters:
            nums (List[int]): The list of integers to check for duplicates.
            k (int): The maximum allowed index difference between duplicate elements.
        
        Returns:
            bool: True if such a duplicate pair exists, otherwise False.
        """
        # Dictionary to store the most recent index of each element.
        last_seen = {}
        
        # Iterate over the list with enumeration to get both index and value.
        for i, num in enumerate(nums):
            # Check if current number has been seen before and if the difference
            # between the current index and the last seen index is within k.
            if num in last_seen:
                # If the index difference is within the given range k, return True.
                if i - last_seen[num] <= k:
                    return True
            # Update the last seen index for the current number.
            last_seen[num] = i
        
        # If no nearby duplicates were found, return False.
        return False
```

**Summary of Techniques and Approaches:**

- **Hash Table for Fast Lookup:** The solution uses a dictionary to quickly store and lookup the most recent index where each number appears, a method broadly applicable when you need to check for duplicates or frequency counts.

- **Single-Pass Iteration:** By processing the array in one iteration, the algorithm maintains an optimal time complexity of O(n), making it suitable for large input sizes. Single-pass approaches are beneficial when performance is critical.

- **Early Exit:** The approach returns immediately upon finding a valid pair, reducing unnecessary computation. This technique is useful for problems where a solution can be determined without fully processing the entire data set.

- **Reusability Across Problems:** The hash table approach is versatile and can be applied to many problems involving lookups, counting frequencies, or checking for conditions over array indices. Always consider hash-based solutions when dealing with duplicate detection or range queries.

- **Conditional Checks Based on Constraints:** The solution checks the range condition right when a duplicate is encountered. This pattern of validating constraints during iteration is a common technique in optimization and constraint satisfaction problems.