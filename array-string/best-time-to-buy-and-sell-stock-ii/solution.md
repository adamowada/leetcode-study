# [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        """
        Calculate the maximum profit from a series of stock prices allowing unlimited transactions.
        
        Parameters:
            prices (List[int]): A list of stock prices where prices[i] is the price on the i-th day.
        
        Returns:
            int: The maximum profit achievable by summing all positive price differences.
        """
        total_profit = 0  # Accumulates the overall profit from transactions
        
        # Iterate from the second day onward, comparing each day's price with the previous day's price.
        for i in range(1, len(prices)):
            # Compute the profit by selling today and having bought yesterday.
            profit = prices[i] - prices[i - 1]
            # If the result is positive, it contributes to the overall profit.
            if profit > 0:
                total_profit += profit
        
        return total_profit
```

**Summary of Techniques and Approaches:**

- **Greedy Strategy:** The solution accumulates profit whenever there is a positive difference between consecutive days. This approach directly captures all profitable opportunities without complex decision-making.
  
- **Single-Pass Iteration:** By iterating once through the list, we achieve O(n) time complexity, a common and efficient pattern for problems involving sequential analysis.

- **Problem Decomposition:** Instead of attempting to identify the best buy and sell points, the problem is simplified by breaking it into daily profit calculations. This technique of breaking a problem into simpler, local decisions can be broadly applied in optimization problems.

- **Applicability:** The greedy, single-pass method is applicable when local optimizations (like immediate profitable moves) lead to a global optimum. Identifying such opportunities can simplify various problems in array manipulation, scheduling, or resource allocation.