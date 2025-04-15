# [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/description/)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        """
        Convert a roman numeral string to an integer.

        Parameters:
            s (str): A string representing a valid Roman numeral.
        
        Returns:
            int: The integer value corresponding to the Roman numeral.
        """
        # Mapping of Roman numeral characters to their integer values.
        numeral_map = {
            'I': 1,    # 1
            'V': 5,    # 5
            'X': 10,   # 10
            'L': 50,   # 50
            'C': 100,  # 100
            'D': 500,  # 500
            'M': 1000  # 1000
        }
        
        total = 0  # This variable will store the final integer result.
        
        # Iterate over each character in the roman numeral string.
        for i in range(len(s)):
            # Check if we are not at the end of the string, and if the current numeral
            # is less than the numeral following it (indicating a subtractive pair).
            if i < len(s) - 1 and numeral_map[s[i]] < numeral_map[s[i+1]]:
                total -= numeral_map[s[i]]  # Subtract if current numeral is a subtractive component.
            else:
                total += numeral_map[s[i]]  # Otherwise, add the numeral's value.
                
        return total
```

**Summary of Techniques and Approaches:**

- **Mapping with a Dictionary:** A dictionary (`numeral_map`) efficiently stores the fixed association between roman numeral characters and integer values. This approach is broadly applicable when a set of inputs maps directly to a set of outputs.

- **Linear Scan with Lookahead:** The solution iterates through the input string once (O(n) time complexity). The use of a lookahead (comparing with the next character) allows handling special subtractive cases elegantly. This technique of scanning with lookahead can be applied to pattern matching and parsing tasks.

- **Conditional Subtraction and Addition:** By checking if the current numeral is less than the next one, the solution determines whether to subtract or add the numeral’s value. This conditional logic is a powerful approach for handling exceptions within sequences and can be applied in scenarios with conditional adjustments.

- **In-Place Computation:** The approach computes the result with constant extra space, demonstrating efficient in-place computation techniques which are useful when memory is limited.

These techniques are useful when solving problems that involve converting between representations, scanning sequences for patterns, and performing conditional operations during one-pass iterations.