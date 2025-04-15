# [27. Remove Element](https://leetcode.com/problems/remove-element/description/)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        """
        Remove all occurrences of 'val' from the list 'nums' in-place.
        
        Parameters:
            nums (List[int]): The list of integers to process.
            val (int): The integer value to remove from the list.
        
        Returns:
            int: The new length of the list 'nums' after removal, where the first k elements
                 contain the values that are not equal to 'val'.
        """
        write_index = 0  # This pointer tracks where the next non-'val' element should be written.
        
        # Iterate through each element in 'nums'
        for num in nums:
            # If the current element does not equal 'val', write it to the current write_index.
            if num != val:
                nums[write_index] = num  # Place the valid element at the 'write_index'
                write_index += 1         # Increment the write_index to the next insertion point
                
        # 'write_index' now represents the count of elements not equal to 'val'
        return write_index
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** The solution uses a slow (write_index) and fast (iteration through nums) pointer. This common approach is efficient for in-place array modifications, as it minimizes additional memory usage.

- **In-Place Data Filtering:** By shifting non-target values forward, the algorithm filters data without the need for extra storage. This technique is broadly applicable to similar problems requiring element removal or partitioning.

- **Single Pass Iteration:** The solution iterates through the list only once, ensuring optimal time complexity of O(n). Look for scenarios where a single-pass algorithm can simplify the solution and improve performance.

- **Application Across Problems:** This method can be applied to various problems involving array partitioning, deduplication, or filtering based on conditions. When you encounter problems that require modifying an array while preserving order (or when order is non-critical), consider leveraging the two-pointer strategy for a clear and elegant solution.