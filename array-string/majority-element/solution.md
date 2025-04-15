# [169. Majority Element](https://leetcode.com/problems/majority-element/description/)

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        """
        Finds and returns the majority element in the list 'nums' using the Boyer-Moore Voting Algorithm.
        
        Parameters:
            nums (List[int]): A non-empty list of integers where the majority element 
                              (an element that appears more than ⌊n/2⌋ times) is guaranteed to exist.
        
        Returns:
            int: The majority element.
        """
        candidate = None  # Holds the current candidate for majority element.
        count = 0         # Counter to track the frequency balance of the candidate.
        
        # Iterate through each number in the input list.
        for num in nums:
            # When count is zero, reset the candidate to the current number.
            if count == 0:
                candidate = num  # Update candidate to the new element.
            # If the current number matches the candidate, increment the count;
            # otherwise, decrement the count.
            if num == candidate:
                count += 1
            else:
                count -= 1
        
        # After processing all numbers, the candidate is the majority element.
        return candidate
```

**Summary of Techniques and Approaches:**

- **Boyer-Moore Voting Algorithm:**  
  This technique is used to find the majority element in a single pass with O(n) time complexity and O(1) space. It efficiently maintains a candidate and a counter to balance occurrences.

- **In-Place Candidate Selection:**  
  The algorithm dynamically selects a candidate by resetting the count when it drops to zero, which is a useful pattern for problems that require identification of a dominant element under constrained space.

- **Single Pass Iteration:**  
  By iterating through the list once, the solution minimizes runtime, which is a principle that can be applied to many problems requiring optimal performance.

- **General Application Tips:**  
  - Use the Boyer-Moore technique when you are guaranteed a majority element or when a similar voting method can be applied.
  - Recognize situations where maintaining a running balance or count (through variables like 'count' and 'candidate') is sufficient to deduce the answer.
  - Look for problems that require in-place processing, especially when the constraints demand minimal extra space.
