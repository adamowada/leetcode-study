# [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word/description/)

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        """
        Return the length of the last word in the string s.
        
        Parameters:
            s (str): An input string consisting of English letters and spaces.
        
        Returns:
            int: The length of the last word in s.
        """
        # Initialize index to the last character of the string.
        i = len(s) - 1
        
        # Skip any trailing spaces at the end of the string.
        while i >= 0 and s[i] == ' ':
            i -= 1
        
        # This counter keeps track of the length of the last word.
        length = 0
        
        # Count the number of characters until we hit a space or the start of the string.
        while i >= 0 and s[i] != ' ':
            length += 1
            i -= 1
        
        # Return the computed length of the last word.
        return length
```

**Summary of Techniques and Approaches:**

- **Backward Traversal:** Instead of splitting the string or using additional memory, the solution traverses the string from the end. This is an effective method when you only care about the trailing segment of data.

- **In-Place Counting:** By using a single index variable and a counter, the solution avoids extra space and keeps the logic straightforward. This pattern is applicable when dealing with sequential data from either end.

- **Handling Edge Cases:** The approach explicitly handles trailing spaces, a common edge case in string manipulation problems. Always consider and remove extraneous characters before processing the main logic.

These techniques are widely applicable in problems where you need to process parts of a sequence or string in a memory-efficient and elegant manner, especially when dealing with end-based calculations.