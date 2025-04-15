# [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        """
        Find the first occurrence of the substring 'needle' in 'haystack' using the KMP algorithm.
        
        Parameters:
            haystack (str): The string in which to search for 'needle'.
            needle (str): The substring to search for in 'haystack'.
        
        Returns:
            int: The index of the first occurrence of 'needle' in 'haystack',
                 or -1 if 'needle' is not found.
        """
        # If needle is an empty string, the problem definition considers its occurrence at index 0.
        if not needle:
            return 0
        
        # Step 1: Preprocess the needle to create the longest prefix suffix (LPS) array.
        lps = [0] * len(needle)  # lps[i] will hold the length of the longest proper prefix that is also a suffix for needle[0:i+1]
        length = 0              # length of the previous longest prefix suffix
        i = 1                   # the LPS for the first character is always 0, so we start with i = 1
        
        # Build the LPS array for the needle.
        while i < len(needle):
            if needle[i] == needle[length]:
                length += 1       # we found a longer prefix which is also suffix
                lps[i] = length   # assign the length to the LPS array for position i
                i += 1
            else:
                if length != 0:
                    # If there is a mismatch, update length to the value of the previous longest prefix suffix.
                    length = lps[length - 1]
                else:
                    # If no proper prefix exists, set lps[i] to 0 and move to the next character.
                    lps[i] = 0
                    i += 1
        
        # Step 2: Use the LPS array to search the needle in the haystack.
        i = 0  # pointer for haystack
        j = 0  # pointer for needle
        
        # Process the haystack while there are characters left.
        while i < len(haystack):
            # If the current characters match, move both pointers.
            if haystack[i] == needle[j]:
                i += 1
                j += 1
            
            # If the entire needle is found, return the start index of the match.
            if j == len(needle):
                return i - j  # Calculate the starting index of the match.
            
            # If a mismatch occurs after j characters matched:
            elif i < len(haystack) and haystack[i] != needle[j]:
                # Use the LPS array to avoid unnecessary comparisons by shifting j.
                if j != 0:
                    j = lps[j - 1]
                else:
                    # Move to the next character in haystack if no prefix to fallback to.
                    i += 1
        
        # If needle is not found in haystack, return -1.
        return -1
```

**Summary of Techniques and Approaches:**

- **KMP (Knuth-Morris-Pratt) Algorithm:**  
  This solution implements the KMP pattern matching algorithm to achieve O(n + m) time complexity, where n is the length of haystack and m is the length of needle. It avoids redundant rechecks by leveraging information from the LPS (longest prefix suffix) array.

- **Preprocessing with LPS Array:**  
  The LPS array is computed for the needle to determine the longest proper prefix which is also a suffix. This array is then used to skip unnecessary comparisons during the search phase, a technique that can be applied to other pattern matching and string searching problems.

- **Two-Phase Approach (Preprocessing and Searching):**  
  The solution is divided into two clear phases: preprocessing to build the LPS array and then searching for the needle in the haystack. This division is useful for breaking down complex problems into manageable sub-problems.

- **General Application:**  
  These techniques are applicable whenever an optimal in-place search or pattern matching is required. When encountering string search problems or scenarios that involve searching within a sequence while minimizing time complexity, consider using or adapting KMP or similar preprocessing strategies.

- **Tips:**  
  - Look for repeating patterns or overlapping sub-problems that can be precomputed.
  - When a straightforward comparison leads to repetitive work, consider algorithms that exploit previous computations.
  - Always analyze the time complexity—optimizing from O(n*m) to O(n + m) can be critical in scaling with input size.