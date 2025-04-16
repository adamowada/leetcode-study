# [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        """
        Find two indices in 'nums' such that the sum of their values equals 'target'.

        Parameters:
            nums (List[int]): A list of integers.
            target (int): The target sum for which two numbers in 'nums' should add up.

        Returns:
            List[int]: A list containing the two indices whose values add up to 'target'.
        """
        # Dictionary to hold the numbers and their indices for quick lookup.
        num_to_index = {}
        
        # Iterate over the list with index and value.
        for i, num in enumerate(nums):
            # Calculate the complement needed to reach the target sum.
            complement = target - num
            
            # Check if the complement exists in our dictionary.
            if complement in num_to_index:
                # If found, return the indices of the complement and the current number.
                return [num_to_index[complement], i]
            
            # Store the current number and its index in the dictionary.
            num_to_index[num] = i

        # Since the problem guarantees exactly one solution, no return is needed here.
```

**Summary of Techniques and Approaches:**

- **Hash Map Utilization:** The solution leverages a hash map (dictionary) for constant-time look-ups to quickly find if the complement of the current number exists. This is useful when trying to achieve an efficient solution in linear time.

- **Single-Pass Algorithm:** By iterating through the list only once, the approach achieves O(n) time complexity. This method is broadly applicable for scenarios where you need to search for pairs or complements within a collection.

- **Space-Time Tradeoff:** Using extra space (dictionary) is an effective tradeoff to reduce time complexity. This technique can be beneficial when the problem constraints allow additional space usage to optimize speed.

- **General Applicability:** This approach can be applied to other problems involving pair-finding (or k-sum variations) and similar scenarios where identifying complementary elements is key. Always consider leveraging hash-based structures for rapid membership checks to optimize performance.