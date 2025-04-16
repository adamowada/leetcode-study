# [289. Game of Life](https://leetcode.com/problems/game-of-life/description/)

```python
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Update the board to its next state according to the Game of Life rules.
        
        Each cell in the board is either live (1) or dead (0). The next state of each cell 
        is determined by its eight neighbors. The update is done in-place by encoding both 
        the original and new state in the same cell using bit manipulation.
        
        Parameters:
            board (List[List[int]]): A 2D list representing the current board state where
                                     each cell is 0 (dead) or 1 (live).
                                     
        The function updates the board in-place and does not return any value.
        """
        if not board or not board[0]:
            return

        m, n = len(board), len(board[0])
        
        # Iterate through each cell to compute the next state.
        # The least significant bit (LSB) holds the current state.
        # The second bit will hold the new state after the update.
        for i in range(m):
            for j in range(n):
                live_neighbors = 0  # Count of live neighbors for board[i][j]
                
                # Check all possible neighbors within bounds.
                for x in range(max(i - 1, 0), min(i + 2, m)):
                    for y in range(max(j - 1, 0), min(j + 2, n)):
                        live_neighbors += board[x][y] & 1  # Only count the original state.
                
                # Exclude the current cell from its neighbor count.
                live_neighbors -= board[i][j] & 1

                # Apply the Game of Life rules:
                # Rule 1 & 3: A live cell dies if it has fewer than 2 or more than 3 live neighbors.
                # Rule 2: A live cell lives on if it has 2 or 3 live neighbors.
                # Rule 4: A dead cell becomes live if it has exactly 3 live neighbors.
                if (board[i][j] & 1 and live_neighbors in (2, 3)) or (board[i][j] == 0 and live_neighbors == 3):
                    board[i][j] |= 2  # Set the 2nd bit to mark the cell as live in the next state
        
        # Update the board to the new state by shifting right to discard the old state.
        for i in range(m):
            for j in range(n):
                board[i][j] >>= 1  # New state is now in the least significant bit.
```

**Summary of Techniques and Approaches:**

- **Bit Manipulation for In-Place Updates:**  
  By encoding both the current and next states within a single integer using bits, we avoid using additional memory and ensure that the state updates occur simultaneously. This method is especially useful when constraints require in-place modifications without extra space.

- **Two-Pass Strategy:**  
  The solution first computes and encodes the new state while retaining the original state for accurate neighbor calculations. A second pass then updates all cells to their new states. This technique can be broadly applied to problems where simultaneous updates or intermediate state preservation is needed.

- **Efficient Neighbor Counting with Bounds Checking:**  
  Iterating over the range of valid neighbors with `max` and `min` functions prevents out-of-bound errors while ensuring every neighboring cell is considered. This approach can be used in many grid-based problems to safely examine adjacent elements.

- **General Problem-Solving Tips:**  
  Look for opportunities to encode multiple pieces of information in a single data structure to reduce space usage. When transitioning between states with dependencies on previous values, consider a staged update process (multi-pass) to avoid interference. These techniques are broadly applicable in dynamic programming, simulations, and state-transition problems.