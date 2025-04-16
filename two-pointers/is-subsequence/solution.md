# [392. Is Subsequence](https://leetcode.com/problems/is-subsequence/description/)

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        """
        Check if string 's' is a subsequence of string 't'.

        Parameters:
            s (str): The string that might be a subsequence of 't'.
            t (str): The target string in which to search for the subsequence.

        Returns:
            bool: True if 's' is a subsequence of 't', False otherwise.
        """
        s_index = 0  # Pointer to track the current index in 's' that we need to match.

        # Iterate through every character in 't'
        for char in t:
            # If there are still characters left in 's' to match and the current character in 't' matches it
            if s_index < len(s) and char == s[s_index]:
                s_index += 1  # Move the pointer forward in 's'
            
            # If all characters in 's' have been matched, 's' is a subsequence of 't'
            if s_index == len(s):
                return True
        
        # Return True if all characters in 's' were matched; otherwise, False.
        return s_index == len(s)
```

**Summary of Techniques and Approaches:**

- **Two-Pointer Technique:** This solution uses two pointers—one to traverse the target string and another to track progression through the potential subsequence. This technique is widely applicable to problems where elements must be matched in order without modifying the original structure.

- **Single-Pass Iteration:** By iterating over the target string only once, the solution achieves an optimal time complexity of O(n), making it efficient for even larger strings.

- **Early Termination:** The condition to exit early once all characters of the subsequence are found can be applied to optimize many algorithms where continuing processing is unnecessary once a goal is reached.

- **Scalability for Multiple Queries:** For scenarios with a large number of queries against a fixed string (the follow-up), a typical approach is to precompute an index mapping for the target string and use binary search to quickly determine the next occurrence of each character. This method reduces the repeated cost of scanning the entire target string for each query.

These techniques can be applied to a variety of sequence and array processing problems, especially when order preservation and efficient in-place modifications are key considerations.