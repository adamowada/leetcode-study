# [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        """
        Remove duplicates from a sorted list 'nums' such that each unique element appears at most twice.
        
        Parameters:
            nums (List[int]): A list of integers sorted in non-decreasing order.
            
        Returns:
            int: The new length of 'nums' after modifying it in-place to allow at most two duplicates per element.
        """
        # If the list has two or fewer elements, no change is needed.
        if len(nums) <= 2:
            return len(nums)
        
        # 'write_index' tracks the position to write the next allowed element.
        # We start from index 2 since the first two elements can always be kept.
        write_index = 2
        
        # Iterate over the list starting from index 2.
        for i in range(2, len(nums)):
            # Check if the current element is different from the element at write_index-2.
            # This ensures that we allow at most two occurrences.
            if nums[i] != nums[write_index - 2]:
                nums[write_index] = nums[i]  # Place the current element at the write_index.
                write_index += 1             # Move to the next write position.
        
        # 'write_index' now represents the new length of the modified list.
        return write_index
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** Utilize one pointer to iterate over the array and another (write_index) to manage in-place overwriting. This minimizes extra space usage and makes the solution efficient.

- **Conditional Check for Duplication:** By comparing the current element with the element at write_index-2, the solution ensures that any element appears at most twice. This idea can be adapted to handle scenarios with different occurrence limits.

- **Single-Pass Iteration:** The algorithm makes only one pass through the array, resulting in O(n) time complexity, which is broadly applicable to many in-place filtering or transformation problems.

- **Pattern Recognition:** The approach emphasizes identifying patterns (e.g., allowed frequency of elements) to decide when and where to place each element, a technique that can be extended to similar problems requiring data filtering or partitioning.