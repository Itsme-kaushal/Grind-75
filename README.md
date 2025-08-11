# LeetCode 11: Container With Most Water

## Problem Overview

Given an integer array `height` of length `n`, there are `n` vertical lines drawn such that the two endpoints of the `i`th line are `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container that can hold the most water.

**Note:** You may not slant the container.

## Thought Process

The key insight is to use the **two-pointer technique**:

1. Start with pointers at both ends of the array (widest possible container)
2. Calculate the current area: `min(height[left], height[right]) * (right - left)`
3. Move the pointer with the smaller height inward
4. Keep track of the maximum area found

**Why move the smaller pointer?**
- The area is limited by the shorter line
- Moving the taller pointer would only decrease width without potential height gain
- Moving the shorter pointer gives us a chance to find a taller line

## Time and Space Complexity

- **Time Complexity:** O(n) - single pass through the array
- **Space Complexity:** O(1) - only using constant extra space

## Solutions

### Python
```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_area = 0
    
    while left < right:
        # Calculate current area
        width = right - left
        current_area = min(height[left], height[right]) * width
        max_area = max(max_area, current_area)
        
        # Move pointer with smaller height
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_area
```

### Java
```java
public int maxArea(int[] height) {
    int left = 0, right = height.length - 1;
    int maxArea = 0;
    
    while (left < right) {
        // Calculate current area
        int width = right - left;
        int currentArea = Math.min(height[left], height[right]) * width;
        maxArea = Math.max(maxArea, currentArea);
        
        // Move pointer with smaller height
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    
    return maxArea;
}
```

### C++
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0, right = height.size() - 1;
        int maxArea = 0;
        
        while (left < right) {
            // Calculate current area
            int width = right - left;
            int currentArea = min(height[left], height[right]) * width;
            maxArea = max(maxArea, currentArea);
            
            // Move pointer with smaller height
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return maxArea;
    }
};
```

## Example

**Input:** `height = [1,8,6,2,5,4,8,3,7]`
**Output:** `49`

**Explanation:** The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`. In this case, the max area of water (blue section) the container can contain is `49`.

## Key Points

- This is a classic two-pointer problem
- The greedy approach works because we always move the pointer that limits our current area
- Alternative brute force approach would be O(n²) - checking all pairs
- This problem teaches the importance of recognizing when greedy algorithms are optimal
