# [15. 3Sum](https://leetcode.com/problems/3sum/description/)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        """
        Find all unique triplets in the list 'nums' that sum up to zero.
        
        Parameters:
            nums (List[int]): The list of integers to search for triplets.
            
        Returns:
            List[List[int]]: A list of lists, where each inner list contains three integers that sum to zero.
        """
        res = []  # This will store the resulting triplets.
        nums.sort()  # Sorting the array to enable the two-pointer technique and easy duplicate skipping.
        
        # Iterate through the array and fix one element at a time.
        for i in range(len(nums) - 2):
            # Skip duplicate elements to avoid repeated triplets.
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            
            # Initialize two pointers, left and right, for the remaining part of the list.
            left, right = i + 1, len(nums) - 1
            
            # Use two pointers to find pairs that sum up with nums[i] to zero.
            while left < right:
                total = nums[i] + nums[left] + nums[right]  # Sum of the fixed element and the two pointers.
                
                # If the sum is less than zero, move the left pointer to increase the sum.
                if total < 0:
                    left += 1
                # If the sum is greater than zero, move the right pointer to decrease the sum.
                elif total > 0:
                    right -= 1
                else:
                    # Found a triplet that sums to zero, add it to the result list.
                    res.append([nums[i], nums[left], nums[right]])
                    
                    # Skip duplicate elements for the left pointer.
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    # Skip duplicate elements for the right pointer.
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    
                    # Move both pointers for the next possible triplet.
                    left += 1
                    right -= 1
        
        # Return the list of unique triplets.
        return res
```

**Summary of Techniques and Approaches:**

- **Sorting:** Sorting the array upfront allows for an organized approach to identify candidate triplets and simplifies the duplicate handling process.
- **Two-Pointer Technique:** By fixing one element and using two pointers for the other elements, the solution efficiently finds pairs that meet the target condition with a time complexity of O(n²).
- **Skip Duplicates:** Careful management of duplicate values prevents the inclusion of redundant triplets, ensuring the result set contains unique combinations.
- **Single Pass over Remaining Elements:** Once the list is sorted, iterating with two pointers in a single pass for each fixed element optimizes the search process.

These techniques are broadly applicable to problems that require finding subsets of elements that satisfy a specific condition, particularly when the input can be sorted to leverage ordering properties, enabling efficient duplicate handling and the two-pointer strategy.