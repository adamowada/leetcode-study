# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        """
        Find the length of the longest substring without repeating characters.
        
        Parameters:
            s (str): The input string consisting of letters, digits, symbols, and spaces.
        
        Returns:
            int: The length of the longest substring that contains no duplicate characters.
        """
        char_index = {}  # Dictionary to store the most recent index of each character.
        longest = 0      # Variable to keep track of the maximum length found.
        start = 0        # Left pointer for the sliding window.

        # Iterate over each character in the string with its index.
        for i, char in enumerate(s):
            # If the character is found in the dictionary and is within the current window,
            # move the start pointer to one position right of its last occurrence.
            if char in char_index and char_index[char] >= start:
                start = char_index[char] + 1
            
            # Update the current character's index in the dictionary.
            char_index[char] = i
            # Calculate the length of the current substring and update longest if needed.
            longest = max(longest, i - start + 1)
        
        return longest
```

**Summary of Techniques and Approaches:**

- **Sliding Window Technique:** This method uses two pointers (start and current index) to maintain a window of unique characters. It's efficient for problems requiring the inspection of contiguous segments in a sequence.
  
- **Hash Map for Fast Lookup:** A dictionary is used to store the latest index of each character, enabling constant time checks for duplicate presence and quick updates to the window's start position.

- **Single Pass Iteration:** The solution processes the string in one pass, resulting in linear time complexity O(n), which is often a target for optimizing performance in similar substring or subarray problems.

- **General Applicability:** This approach can be applied to a range of problems where one needs to find the longest subsegment under specific constraints (e.g., subarrays with a given sum, subarrays with distinct elements). Look for opportunities to use the sliding window when the problem involves continuous sections of an array or string, and consider hash maps for scenarios that require fast membership checks or frequency counts.