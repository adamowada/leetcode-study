# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        """
        Returns an array 'answer' where each element at index i is the product of all the elements
        in the input list 'nums' except nums[i]. The solution runs in O(n) time and uses O(1) extra
        space (excluding the output array).
        
        Parameters:
            nums (List[int]): List of integers for which the product excluding the current element
                              is calculated.
        
        Returns:
            List[int]: Array where each element is the product of all other elements in 'nums' except
                       the element at the corresponding index.
        """
        n = len(nums)
        answer = [1] * n  # Initialize the answer array with 1s.

        # Left pass: Compute the cumulative product of all elements to the left of each index.
        left_product = 1  # This variable will hold the product of elements to the left of the current index.
        for i in range(n):
            answer[i] = left_product  # Set the current answer as the product of all elements to the left.
            left_product *= nums[i]   # Update left_product with the current element.

        # Right pass: Compute the cumulative product of all elements to the right and multiply it with the left product.
        right_product = 1  # This variable will hold the product of elements to the right of the current index.
        for i in range(n - 1, -1, -1):
            answer[i] *= right_product  # Multiply the stored left product with the right cumulative product.
            right_product *= nums[i]    # Update right_product with the current element.

        return answer
```

**Summary of Techniques and Approaches:**

- **Two-Pass Cumulative Product:** The solution calculates products in two passes over the array—first computing left cumulative products and then right cumulative products, which are combined to produce the final result. This strategy is beneficial when a problem can be decomposed into independent sub-problems whose results can be merged.

- **In-Place Computation (O(1) Extra Space):** By reusing the output array for storing intermediate left products and then combining with right products, the approach minimizes extra space usage. This technique is widely applicable in problems where modifying or building the result in-place is advantageous.

- **Single-Pass Updates with Accumulators:** Using accumulators to keep track of cumulative products is a technique that can be applied to many problems involving prefix, suffix, or rolling window computations. Recognizing when to use accumulators can lead to efficient, single-pass algorithms.

- **Avoiding Division:** The solution circumvents the pitfalls of division by using multiplication, which is essential in scenarios where division might lead to precision issues or when division is explicitly forbidden.

These techniques offer a framework for solving similar array manipulation and cumulative computation problems efficiently and elegantly.