# [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        """
        Validate a 9x9 Sudoku board by ensuring that each row, column,
        and 3x3 sub-box contains no duplicate digits from '1' to '9'.

        Parameters:
            board (List[List[str]]): A 9x9 grid represented as a list of lists,
                                     where each cell is a digit '1'-'9' or '.' indicating an empty cell.

        Returns:
            bool: True if the board is valid according to Sudoku rules,
                  False otherwise.
        """
        seen = set()  # A set to store seen digits with unique keys for rows, columns, and sub-boxes
        
        # Loop over each row index in the board
        for i in range(9):
            # Loop over each column index in the board
            for j in range(9):
                digit = board[i][j]  # Current cell value
                if digit != '.':     # Process only non-empty cells
                    # Create unique identifiers for the digit's occurrence in the row, column, and box
                    row_key = (i, digit)          # Uniquely identifies digit in row i
                    col_key = (j, digit)          # Uniquely identifies digit in column j
                    box_key = (i // 3, j // 3, digit)  # Uniquely identifies digit in its 3x3 sub-box
                    
                    # If any of these keys already exists in 'seen', the board is invalid
                    if row_key in seen or col_key in seen or box_key in seen:
                        return False
                    
                    # Record the digit's occurrence for row, column, and sub-box validation
                    seen.add(row_key)
                    seen.add(col_key)
                    seen.add(box_key)
                    
        # If no duplicates are found, the board is valid
        return True
```

**Summary of Techniques and Approaches:**

- **Single-pass Validation with Hashing:**  
  By iterating through each cell only once and using a hash set, we efficiently track the unique occurrence of digits across rows, columns, and sub-boxes. This minimizes both time and space overhead.

- **Unified Data Structure for Multiple Constraints:**  
  We encode the different constraints (row, column, sub-box) as distinct tuple keys. This approach allows using a single set to enforce multiple uniqueness rules, which is widely applicable for problems involving multiple overlapping conditions.

- **Modular and Readable Code:**  
  Including clear inline comments and a comprehensive docstring aids in maintainability and learning. This technique is useful when approaching complex problems since it breaks down the logic into understandable steps.

- **Application Tips:**  
  Look for scenarios where you need to validate or partition data based on multiple criteria. Use data structures like sets or dictionaries to track occurrences and identify conflicts quickly, and consider how to encode multiple rules into a single unified check.