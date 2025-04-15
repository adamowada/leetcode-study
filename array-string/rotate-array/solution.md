# [189. Rotate Array](https://leetcode.com/problems/rotate-array/description/)

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Rotate the list 'nums' to the right by 'k' steps in-place.

        Parameters:
            nums (List[int]): The list of integers to be rotated.
            k (int): The number of steps to rotate the list.

        This function modifies 'nums' in-place by first reversing the entire list,
        then reversing the first k elements, and finally reversing the remaining
        elements. This approach uses O(1) extra space.
        """
        n = len(nums)
        # If the list is empty or no rotation is needed, exit early.
        if n == 0:
            return
        
        # Normalize k to ensure it is within the bounds of the list's length.
        k %= n
        
        # Helper function to reverse elements of nums between indices 'left' and 'right' inclusive.
        def reverse(left: int, right: int) -> None:
            while left < right:
                # Swap the elements at indices 'left' and 'right'.
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        
        # Step 1: Reverse the entire list.
        reverse(0, n - 1)
        # Step 2: Reverse the first k elements to restore their original order.
        reverse(0, k - 1)
        # Step 3: Reverse the remaining n - k elements to restore their original order.
        reverse(k, n - 1)
```

**Summary of Techniques and Approaches:**

- **Reversal Technique:** The solution rotates the array using three reversals—a method that inverts the entire array, then individually restores the order of the rotated parts. This approach is broadly applicable to in-place array manipulation problems.

- **Modulo Arithmetic:** Reducing k with `k %= n` ensures that the number of rotations is within the array's bounds, a useful trick for cyclic or repetitive transformations.

- **In-Place Modification:** The method employs constant extra space by rearranging elements within the original list, a key technique when memory efficiency is crucial.

- **Helper Function Abstraction:** Using a helper function (reverse) not only encapsulates a common operation but also improves readability and reusability in various array manipulation contexts.

These techniques are powerful in many scenarios, such as cyclic shifts, array partitioning, or problems requiring optimization of space usage.