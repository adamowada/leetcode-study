# [155. Min Stack](https://leetcode.com/problems/min-stack/description/)

```python
class MinStack:
    """
    A stack data structure that supports push, pop, top, and retrieving 
    the minimum element in constant time.
    
    Attributes:
        stack (List[int]): The primary list storing all stack elements.
        min_stack (List[int]): A secondary list that keeps track of the 
                               current minimum element at each level of the stack.
    """
    def __init__(self):
        """
        Initialize the MinStack.
        """
        self.stack = []      # Primary stack to store the elements.
        self.min_stack = []  # Secondary stack to maintain current minimum for each push.

    def push(self, val: int) -> None:
        """
        Pushes the element 'val' onto the stack and updates the minimum stack.
        
        Parameters:
            val (int): The value to be pushed onto the stack.
        """
        # Add the element to the main stack.
        self.stack.append(val)
        # If min_stack is empty or the current value is smaller or equal to the last minimum, push it to min_stack.
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        """
        Removes the element on the top of the stack and updates the minimum stack accordingly.
        """
        # Pop the top element from the main stack.
        popped = self.stack.pop()
        # If the popped element is the current minimum, also pop it from the min_stack.
        if popped == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self) -> int:
        """
        Retrieves the top element of the stack without removing it.
        
        Returns:
            int: The top element of the stack.
        """
        return self.stack[-1]

    def getMin(self) -> int:
        """
        Retrieves the minimum element in the stack in constant time.
        
        Returns:
            int: The current minimum element in the stack.
        """
        return self.min_stack[-1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

**Summary of Techniques and Approaches:**

- **Two-Stack Method:** We maintain two stacks: one for all the elements and another dedicated to tracking the current minimum element. This pattern allows constant time updates and retrieval of the minimum.

- **Conditional Updates:** In the `push` method, the new value is compared with the current minimum, and if it's smaller or equal, it is pushed onto the min_stack. This conditional update ensures that the min_stack always reflects the smallest element in the current stack.

- **Synchronized Pop Operations:** When popping, the value is removed from both stacks if it is the current minimum. This synchronization between the two stacks maintains the integrity of the minimum tracking.

- **General Application Tips:** 
  - Use auxiliary data structures to track additional state (like minimum, maximum, or frequency) when performing operations in constant time.
  - Apply the two-pointer or dual data structure concept when you need to compute dynamic properties (e.g., minima, maxima) as the dataset changes.
  - Look for opportunities to leverage conditional logic on data structure operations to carry extra metadata that can be reused efficiently in future operations.