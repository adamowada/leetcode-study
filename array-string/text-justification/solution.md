# [68. Text Justification](https://leetcode.com/problems/text-justification/description/)

```python
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        """
        Format a list of words so that each line has exactly maxWidth characters and is fully justified.
        
        Parameters:
            words (List[str]): A list of words (strings) to be formatted.
            maxWidth (int): The number of characters each line must have.
        
        Returns:
            List[str]: A list of justified text lines where all lines except possibly the last are fully justified.
                     The last line is left-justified.
        """
        result = []     # Final list of justified lines.
        i = 0           # Starting index for words in the current line.
        n = len(words)  # Total number of words.
        
        # Process words until we've processed all of them.
        while i < n:
            j = i              # j will represent the end (exclusive) index for the current line.
            current_line_length = 0  # Total length of words in the current line (excluding spaces).
            
            # Determine how many words can be added to the current line.
            # (j - i) represents the count of spaces needed between the words already added.
            while j < n and current_line_length + len(words[j]) + (j - i) <= maxWidth:
                current_line_length += len(words[j])
                j += 1
            
            num_words = j - i  # Number of words in the current line.
            line = ""
            
            # If this is the last line or the line contains only one word, left justify.
            if j == n or num_words == 1:
                # Join the words with a single space.
                line = " ".join(words[i:j])
                # Pad the remaining space to reach maxWidth.
                line += " " * (maxWidth - len(line))
            else:
                # Calculate the total number of spaces to distribute.
                total_spaces = maxWidth - current_line_length
                # Evenly distribute spaces between words.
                space_per_gap = total_spaces // (num_words - 1)
                # Extra spaces that cannot be evenly distributed.
                extra_spaces = total_spaces % (num_words - 1)
                
                # Build the justified line.
                for k in range(i, j - 1):
                    line += words[k]
                    # Distribute one extra space for the leftmost gaps if needed.
                    spaces_to_add = space_per_gap + (1 if k - i < extra_spaces else 0)
                    line += " " * spaces_to_add
                # Append the last word without additional spaces.
                line += words[j - 1]
            
            # Add the formatted line to the result list.
            result.append(line)
            # Move to the next segment of words.
            i = j
        
        return result
```

**Summary of Techniques and Approaches:**

- **Greedy Word Packing:** The solution packs as many words as possible into a line without exceeding the maximum width, a strategy useful in many scheduling or packing problems.

- **Two-Phase Processing:** First, determine the group of words for each line, then format them by distributing spaces. This separation of concerns simplifies handling of both grouping and formatting.

- **Space Distribution:** When a line is not the last line and contains more than one word, the algorithm calculates the base number of spaces to insert between each pair of words, and then distributes extra spaces from left to right. This evenly distributes the required padding and is a pattern that can be applied in load balancing or resource distribution problems.

- **Edge Case Handling:** Special cases, such as the last line or a line with a single word, are handled differently (left-justified) to meet specific problem requirements. Recognizing and addressing edge cases is crucial in algorithm design.

These techniques—greedy selection, two-phase processing, balanced distribution, and careful edge-case handling—are widely applicable in solving various data processing and optimization problems.