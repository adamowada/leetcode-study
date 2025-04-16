# [30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/)

```python
class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        """
        Finds all starting indices in 's' where a concatenation of each word in 'words' exactly once occurs.

        Parameters:
            s (str): The input string in which to search for concatenated substrings.
            words (List[str]): A list of words, all of the same length, to be concatenated in any permutation.

        Returns:
            List[int]: A list of starting indices of the concatenated substrings in 's'.
        """
        if not s or not words:
            return []
        
        word_len = len(words[0])            # Length of each word; all words are of equal length.
        num_words = len(words)              # Total number of words in the list.
        total_len = word_len * num_words    # Total length of concatenated substring.
        s_len = len(s)                      # Length of the input string.
        
        # Build a frequency dictionary for the words in 'words'
        word_count = {}
        for word in words:
            word_count[word] = word_count.get(word, 0) + 1
        
        indices = []
        # We loop over word_len different starting offsets.
        for i in range(word_len):
            left = i                   # Left pointer for the sliding window.
            count = 0                  # Number of valid words seen in the current window.
            seen = {}                  # Frequency dictionary for words seen in the current window.
            
            # Slide window in steps of word_len
            for j in range(i, s_len - word_len + 1, word_len):
                word = s[j:j + word_len]  # Extract a word-sized substring.
                
                # Check if the extracted word is part of the desired words
                if word in word_count:
                    seen[word] = seen.get(word, 0) + 1
                    count += 1  # Increase count of words seen in window
                    
                    # If word frequency exceeds required frequency, shrink the window from the left.
                    while seen[word] > word_count[word]:
                        left_word = s[left:left + word_len]
                        seen[left_word] -= 1
                        left += word_len
                        count -= 1
                    
                    # If the window has exactly the number of words required, record the starting index.
                    if count == num_words:
                        indices.append(left)
                        # Move the window forward by removing the leftmost word.
                        left_word = s[left:left + word_len]
                        seen[left_word] -= 1
                        left += word_len
                        count -= 1
                else:
                    # If the word isn't in the given list, reset the window.
                    seen.clear()
                    count = 0
                    left = j + word_len
        
        return indices
```

**Summary of Techniques and Approaches:**

- **Sliding Window with Multiple Offsets:**  
  The solution uses a sliding window that is adjusted based on the fixed word length. Scanning with different starting offsets ensures every possible concatenation alignment is considered. This method is applicable in substring search problems where fixed-length segments are involved.

- **Hash Map for Frequency Counting:**  
  By building and comparing frequency dictionaries for the target words and the current window, the algorithm efficiently tracks whether the current substring is a valid concatenation. This technique is broadly applicable in problems requiring pattern matching or checking anagram conditions.

- **Dynamic Window Adjustment:**  
  When the frequency of a word in the current window exceeds the required count, the algorithm incrementally moves the left pointer to restore validity. This approach of dynamically adjusting the window size is useful in many scenarios where you need to find a contiguous segment meeting specific criteria.

- **Modular Iteration:**  
  Iterating over different initial offsets (from 0 to word_len - 1) ensures that all potential starting positions are considered without redundant checks. This technique can be used in various problems where grouping or segmentation based on a fixed step is beneficial.

These techniques, when recognized and applied, are powerful tools for efficiently solving a wide range of substring and pattern matching problems in algorithm challenges.