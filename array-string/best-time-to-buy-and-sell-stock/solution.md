# [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        """
        Calculate the maximum profit from a single buy and sell transaction given stock prices.
        
        Parameters:
            prices (List[int]): List of stock prices where prices[i] is the price on day i.
        
        Returns:
            int: The maximum profit achievable by buying on one day and selling on a later day.
                 Returns 0 if no profit can be made.
        """
        # Initialize minimum price to a large value and maximum profit to 0.
        min_price = float('inf')  # This variable holds the lowest price observed so far.
        max_profit = 0            # This variable holds the maximum profit computed so far.
        
        # Iterate over each price in the list.
        for price in prices:
            # If the current price is lower than the recorded minimum, update the minimum price.
            if price < min_price:
                min_price = price  # Update with the new minimum price.
            
            # Calculate the potential profit by subtracting the minimum price from the current price.
            profit = price - min_price
            
            # If this profit is higher than the recorded maximum profit, update the maximum profit.
            if profit > max_profit:
                max_profit = profit  # Update with the new maximum profit.
        
        # Return the maximum profit achievable.
        return max_profit
```

**Summary of Techniques and Approaches:**

- **Single-Pass Greedy Approach:** The solution processes the list once, updating the minimum price encountered and calculating the profit on the fly, ensuring an optimal O(n) time complexity.
- **State Tracking with Variables:** Maintaining variables for the minimum price and maximum profit allows for efficient computation without extra space, a common technique in in-place optimization problems.
- **Identifying Problem Patterns:** Recognize that many problems can be solved by tracking a running minimum (or maximum) and comparing it against current values to decide on updates, a strategy applicable in problems like array partitioning or window-based optimization.
- **Simplification by Eliminating Redundancies:** The solution elegantly avoids nested loops by relying on straightforward conditional checks, applicable whenever you need to derive the best result from sequential data.