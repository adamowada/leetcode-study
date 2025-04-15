# [134. Gas Station](https://leetcode.com/problems/gas-station/description/)

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        """
        Determines the starting gas station index to complete the circuit or returns -1 if not possible.
        
        Parameters:
            gas (List[int]): List containing the amount of gas available at each station.
            cost (List[int]): List containing the cost of gas to travel to the next station.
        
        Returns:
            int: The starting station's index if the circuit can be completed; otherwise, -1.
        """
        total_tank = 0   # Overall gas surplus across all stations.
        current_tank = 0 # Current gas surplus for the ongoing simulation from candidate start.
        start = 0        # Candidate starting station.
        
        # Iterate through each station to simulate traveling.
        for i in range(len(gas)):
            diff = gas[i] - cost[i]  # Net gas after leaving station i.
            total_tank += diff       # Update overall surplus/deficit.
            current_tank += diff     # Update running surplus for current starting candidate.
            
            # If current_tank is negative, the current start cannot reach station i+1.
            if current_tank < 0:
                start = i + 1      # Change candidate start to the next station.
                current_tank = 0   # Reset the current surplus.
        
        # If overall gas is sufficient, return the candidate start; otherwise, return -1.
        return start if total_tank >= 0 else -1
```

**Summary of Techniques and Approaches:**

- **Greedy Algorithm:** The solution leverages a greedy strategy that checks each station sequentially. If the running gas balance (current_tank) falls below zero, it discards the current candidate start and selects the next station. This pattern is useful for optimizing problems where local decisions lead to a global optimum.

- **Simulation and Accumulation:** By iterating through the stations and cumulatively calculating the surplus (or deficit), the solution efficiently simulates the journey. This accumulation approach is broadly applicable when you need to verify overall feasibility before refining the starting point.

- **Overall Feasibility Check:** The algorithm first calculates the total gas surplus (total_tank) to determine if the journey is possible at all. This principle—verifying global conditions before detailed simulation—can be applied to many optimization and feasibility problems.

- **Application Tips:** Use these techniques when a problem involves cyclic routes, sequential decision-making, or when you need to track cumulative conditions. The two-pronged approach of checking global feasibility and then simulating the journey provides clarity and efficiency for similar problems.