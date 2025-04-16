# [228. Summary Ranges](https://leetcode.com/problems/summary-ranges/description/)

```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        """
        Summarizes contiguous ranges in a sorted unique integer array.
        
        Parameters:
            nums (List[int]): A sorted list of unique integers.
        
        Returns:
            List[str]: A sorted list of ranges covering all the numbers in nums.
                       Each range is represented as "a->b" if a != b or "a" if a == b.
        """
        ranges = []         # List to hold the final string representation of ranges.
        n = len(nums)       # Total number of elements in the input list.
        i = 0               # Index pointer for traversing nums.
        
        # Traverse the list to find and format contiguous ranges.
        while i < n:
            start = nums[i]  # Start of the current range.
            
            # Move the pointer while the consecutive numbers continue.
            while i + 1 < n and nums[i + 1] == nums[i] + 1:
                i += 1  # Increment the pointer to include the contiguous number.
            
            end = nums[i]   # End of the current contiguous range.
            
            # Format the range: if there's only a single number, no arrow is used.
            if start == end:
                ranges.append(f"{start}")
            else:
                ranges.append(f"{start}->{end}")
            
            i += 1  # Proceed to the next element beyond the current range.
        
        return ranges
```

**Summary of Techniques and Approaches:**

- **Two-Pointer/Single-Pass Iteration:** The solution uses a pointer to traverse the sorted list only once. It leverages the sorted order to efficiently identify contiguous sequences by checking if the next element is exactly one greater than the current element.

- **In-Place Grouping:** By recording the start and end of each contiguous sequence as soon as the break in continuity is detected, the solution elegantly groups numbers into ranges without extra data structures or multiple passes.

- **Conditional Formatting:** The solution demonstrates the importance of formatting output based on conditions—in this case, choosing between a single-number string and a range string.

- **General Applicability:** Techniques like single-pass iteration and conditional aggregation can be applied to a variety of problems such as detecting intervals in time-series data, summarizing ranges in datasets, or partitioning an array based on a predicate. When facing problems involving sequential or contiguous elements, consider using these approaches to simplify and optimize your solution.