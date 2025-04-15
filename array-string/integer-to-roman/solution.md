# [12. Integer to Roman](https://leetcode.com/problems/integer-to-roman/description/)

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        """
        Convert an integer to its Roman numeral representation.
        
        Parameters:
            num (int): An integer between 1 and 3999.
            
        Returns:
            str: The Roman numeral representation of the integer.
        """
        # Map integer values to their corresponding Roman numeral symbols,
        # including subtractive forms to handle special cases.
        roman_mappings = [
            (1000, "M"), (900, "CM"), (500, "D"), (400, "CD"),
            (100, "C"), (90, "XC"), (50, "L"), (40, "XL"),
            (10, "X"), (9, "IX"), (5, "V"), (4, "IV"), (1, "I")
        ]
        
        result = []  # This list will store parts of the resulting Roman numeral.
        
        # Iterate over each numeral from largest to smallest.
        for value, symbol in roman_mappings:
            if num >= value:
                count = num // value  # Determine how many times the numeral fits into num.
                result.append(symbol * count)  # Append the symbol repeated 'count' times.
                num -= value * count  # Decrease num by the total amount converted.
                
        # Combine all parts into a single string representing the Roman numeral.
        return "".join(result)
```

**Summary of Techniques and Approaches:**

- **Greedy Algorithm:** The solution uses a greedy approach by iterating over numeral values from highest to lowest, subtracting the largest possible value at each step. This approach is effective for problems where making a local optimal choice (largest numeral that fits) leads to a global solution.

- **Mapping with Precomputed Pairs:** Using a list of tuples to map integer values to their Roman numeral symbols—including subtractive forms—simplifies the conversion process. This technique is widely applicable when solving problems that involve conversion between systems or representations.

- **Iterative Reduction:** The algorithm iteratively reduces the input number by accounting for the contributed value at each step. This technique can be applied in other problems where a quantity needs to be decomposed into parts (e.g., coin change problems).

- **In-Place String Construction:** Building the result using a list that is joined into a final string is both elegant and efficient. This pattern is useful for scenarios where concatenation of multiple components is required.

These techniques provide a framework that can be applied to similar problems involving greedy strategies, mapping-based conversions, and iterative processing.