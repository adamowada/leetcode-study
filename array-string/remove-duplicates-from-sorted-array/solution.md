# [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        """
        Remove duplicates from a sorted list in-place so that each unique element appears only once,
        maintaining the original order. Returns the number of unique elements.
        
        Parameters:
            nums (List[int]): The sorted list of integers from which duplicates are removed.
            
        Returns:
            int: The number of unique elements after duplicates have been removed.
        """
        # If the list is empty, return 0 unique elements.
        if not nums:
            return 0
        
        # write_index points to the position where the next unique element should be placed.
        write_index = 1  # Start from 1 since the first element is always unique.
        
        # Iterate through the list starting from the second element.
        for i in range(1, len(nums)):
            # If the current element is not the same as the previous element,
            # it is a unique element that should be kept.
            if nums[i] != nums[i - 1]:
                nums[write_index] = nums[i]  # Write the unique element at the write_index.
                write_index += 1            # Increment write_index for the next unique element.
                
        # write_index now equals the number of unique elements in the list.
        return write_index
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** The solution employs two pointers: one for reading through the list and one for writing unique elements. This is a common pattern for in-place array modifications when trying to minimize extra space usage.

- **In-Place Filtering:** By checking adjacent elements (relying on the sorted property), the approach efficiently filters out duplicates without using additional space. This technique applies broadly to scenarios where array modifications must be done in place.

- **Single-Pass Iteration:** Iterating the list only once results in O(n) time complexity, an optimal solution for problems involving traversal and filtering of arrays. Look for opportunities to exploit data ordering (like sorted arrays) to apply similar strategies in other problems.